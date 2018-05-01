---
title: aio mode
date: 2017-04-07 17:06:59
tags: qemu
---

  compare and conclude two aio modes on qemu: native and threads

<!-- more -->

## native
  just use linux aio: libaio, invoke io_submit to submit requests to kernel

## threads
  use qemu thread pool to emulate asynchronized I/O, the start routine of threads to submit requests to kernel is aio_worker[block/raw-posix.c: 1150], and aio_worker invokes pread/pwrite, preadv/pwritev, and etc

## entry
                            aw_co_prw
                                |
                        --------v--------
                        |               |
                        v               v
                 laio_co_submit  paio_submit_co

## native routine
    latio_co_submit
        |
        +-laio_do_submit
            |
            |-io_prep_pwritev/io_prep_preadv
            |
            +-ioq_submit
                |
                +-io_submit

## threads routine
    paio_submit_co
        |
        +-thread_pool_submit_co
            |
            +-thread_pool_submit_aio
                .
                .
                .(on worker thread)
                +-aio_woker
                    |
                    +-handle_aiocb_rw
                        |
                        +-handle_aiocb_rw_linear / handle_aiocb_rw_vector
                            |                        |
                            +-pwrite/pread           +-qemu_pwritev/qemu_preadv
                                                         |
                                                         +-pwritev/preadv

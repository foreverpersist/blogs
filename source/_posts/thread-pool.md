---
title: thread pool
date: 2017-04-07 17:07:26
tags: qemu
---

  explain how qemu thread pool works

<!-- more -->

## Structure

### ThreadPool

#### completion_bh
  invoke thread_pool_completion_bh to handle respones after a request has been handled

#### new_thread_bh
  invoke spawn_thread_bh_fn to create threads if needed

#### max_threads 
  max thread num

#### cur_threads 
  current thread num include threads which will be created

#### idle_threads
  idle threads num

#### pending_threads 
  pending thread num


## API
### thread_pool_submit_aio 
>* insert a req to request list 
>* if there no idle threads, cur_threads and new_threads is increased, and do_spawn_thread will be invoked if there are no pending threads

### do_spawn_thread
>* if there are threads needed to be created, new_threads is decreased, pending_threads is increased, and a new threads will be created with start routine worker_thread

### worker_thread
>* pending_threads is decreased
>* invoke do_spawn_thread to handle new_threads

>* loop: until thread pool stops or error happens
>>* inner loop: until a request arrives
>>* idle_threads is increased
>>* wait for request with timeout 10000
>>* idle_threads is decreased

>* get a request form request list and handle it by executing req->func
>* schedule completion_bh to invoke thread_pool_completion_bh
>* cur_threads is decreased

### thread_pool_completion_bh
>* restart(tag):
>>* find a element whose start is THREAD_DONE
>>* remove the element
>>* if the element has own compleltion function, it will be invoked, then the element will be released and 'restart' will be executed again; otherwise, the element will be released

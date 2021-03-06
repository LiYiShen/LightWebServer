
线程同步机制包装类
===============
多线程同步，确保任一时刻只能有一个线程能进入关键代码段。类中主要是对Linux下三种锁进行封装，将锁的创建和销毁函数封装在类的构造与析构函数中，实现RAII机制。
> * 信号量
- P，如果SV的值大于0，则将其减一；若SV的值为0，则挂起执行
- V，如果有其他进行因为等待SV而挂起，则唤醒；若没有，则将SV值加一
- `sem_init`函数用于初始化一个未命名的信号量
- `sem_destory`函数用于销毁信号量
- `sem_wait`函数将以原子操作方式将信号量减一,信号量为0时,sem_wait阻塞
- `sem_post`函数以原子操作方式将信号量加一,信号量大于0时,唤醒调用sem_post的线程
> * 互斥锁
- `pthread_mutex_init`函数用于初始化互斥锁
- `pthread_mutex_destory`函数用于销毁互斥锁
- `pthread_mutex_lock`函数以原子操作方式给互斥锁加锁
- `pthread_mutex_unlock`函数以原子操作方式给互斥锁解锁
> * 条件变量
- `pthread_cond_init`函数用于初始化条件变量
- `pthread_cond_destory`函数销毁条件变量
- `pthread_cond_broadcast`函数以广播的方式唤醒所有等待目标条件变量的线程
- `pthread_cond_wait`函数用于等待目标条件变量.该函数调用时需要传入 mutex参数(加锁的互斥锁) ,函数执行时,先把调用线程放入条件变量的请求队列,然后将互斥锁mutex解锁,当函数成功返回为0时,互斥锁会再次被锁上. 也就是说函数内部会有一次解锁和加锁操作.





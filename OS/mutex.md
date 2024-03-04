

> 互斥锁用于保护***临界区***的资源一次只能被一个线程访问（或修改），用于***线程同步***。



> 互斥锁的类型是`pthread_mutex_t`结构体

```c
typedef struct
{
    int m_spinlock;                    // 自旋锁
    int m_count;                       // 用于递归加锁，记录某线程获取该锁的次数
    pthread_t m_owner;                 // 记录是谁获取了互斥量
    int m_kind;                        // 互斥量类型，递归或非递归
    struct _pthread_queue m_waiting;   // 等待互斥量的线程队列
}pthread_mutex_t; 
```



> `init`



> `lock`

阻塞

> `unlock`



> `destroy`



> `trylock`

不阻塞
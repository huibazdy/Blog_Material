

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

>





> 线程共享进程的那些资源

1. 文件描述符
2. 全局内存
3. 堆内存
4. 栈内存
5. 寄存器
6. 可执行程序的代码



> 线程接口——**pthread**（即：**POSIX.1-2001**）

```c
#ifdef _POSIX_THREADS   // 编译时确认是否支持该线程接口（即是否支持 pthread）
...
#endif
```



> PID  和 TID



|         | 类型      | 唯一性                   |      |
| ------- | --------- | ------------------------ | ---- |
| 进程 ID | pid_t     | 整个系统中唯一           |      |
| 线程 ID | pthread_t | 所属进程上下文中才有意义 |      |


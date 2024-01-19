> fork 的返回值

fork 被调用一次但返回两次：

1. 向调用者（父进程）返回新建子进程的 PID

    因为一个进程的子进程可以有多个，且没有函数可以返回一个进程的所有子进程 PID。

2. 向新建子进程返回 0 

    理解为子进程也执行一次fork语句，但不创建任何实际新进程。

综上，我们可以根据fork返回值来判断当前进程是子进程还是父进程。



> 怎样理解子进程是父进程的副本







> 调用fork之后？

父进程和子进程都开始执行fork语句之后的代码，之前的代码父进程已经执行完毕





> 一个实例



```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main()
{
    pid_t pid = fork();
    if(pid < 0)
        printf("Fail to fork");
    else if(pid == 0)
        printf("Child pid = %d\n",getpid());
    else if(pid > 0)
        printf("Parent pid = %d\n",getpid());
    return 0;
}
```
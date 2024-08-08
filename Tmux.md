# Tmux

## 终端基本概念

### 会话

打开终端窗口，用户通过它与计算机交互。这个窗口建立的是一次“会话”（session）。会话的特点是：与窗口中的进程捆绑，关闭窗口意味着会话结束，会话内的进程也随之终止，无论该进程是否运行完。

### 解绑

将窗口与会话解绑，这样关闭窗口就不会终止会话（会话中的进程继续运行），等到之后需要时，再让会话“绑定”其他窗口。



## Tmux

### Tmux 简介

**Tmux** 就是一个用于将终端窗口与会话解绑的工具。这样做的常见效果有：

1. 允许单个窗口同时访问多个会话，对同时运行多个命令行程序很必要；
2. 可以让新创建窗口与已存在的会话绑定；
3. 支持窗口水平和垂直拆分；
4. 允许单个会话同时连接多个窗口，因此可以多人实时共享会话；



### Tmux 基本使用

#### 1. 进入和退出

```shell
tmux  #进入
exit  #退出
```

进入后最下方会有一个高亮状态栏，左侧是窗口信息：编号（第一个打开的窗口是 0）和名称；有测试系统信息。



#### 2. 新建会话

新建会话同时命名会话，如果不指定名称则默认用编号（几号会话）命名

```shell
tmux new -s <session-name>
```



#### 3. 分离会话

将当前会话与窗口解绑，执行完后会退出当前 Tmux 窗口，但会话和其中进程仍在后台运行。

```shell
tmux detach
```



#### 4. 查看会话

查看所有 Tmux 会话

```shell
tmux ls
```



#### 5. 接入会话

```shell
tmux attach -t <session_number>  #使用编号接入
tmux attach -t <session_name>    #使用名称接入
```



#### 6. 杀死会话

```shell
tmux kill-session -t <session_number>  #使用编号
tmux kill-session -t <session_name>    #使用名称
```



#### 7. 切换会话

```shell
tmux switch -t <session_number>  #使用编号
tmux switch -t <session_name>    #使用名称
```



#### 8. 重命名会话

```shell
tmux rename-session -t  <session_number> <new_name>  #使用编号
tmux rename-session -t <old_name> <new_name>         #使用名称
```



### Tmux 窗口管理

#### 1. 划分窗口

```shell
tmux split-window         #划分为上下两个
tmux split-window -h      #划分为左右两个
```



#### 2. 移动光标

```shell
tmux select-pane -U    #上窗口
tmux select-pane -D    #下窗口
tmux select-pane -L    #左窗口
tmux select-pane -R    #右窗口
```



## 参考资料

1. [阮一峰的博客](https://www.ruanyifeng.com/blog/2019/10/tmux.html)
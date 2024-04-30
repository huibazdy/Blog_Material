## 临时配置

> 临时配置在命令模式（`:`）下使用`set`命令实现，只在当前vim打开的文件中生效，关闭后重新打开失效。

* **显示行号**
    * `:set nu`
    * `:set nonu`
* **缩进**
    * `:set tabstop=4`（设置Tab键宽度为4个空格）
    * `:set autoindent`（设置自动缩进，即每行缩进与上一行相同）
* **设置编码格式**
    * `:set encoding=utf-8`（用于缓存的文本、寄存器、vim脚本文件等）
    * `:set fileencoding=utf-8,ucs-bom,gb18030,gbk,gb2312,cp936`（vim写入文件时采用的编码）
    * `:set termencoding`（从vim输出到终端时采用的编码）
* **当前行高亮**
    * `:set cursorline`
* **启动鼠标**
    * `:set mouse=a`
    * `:set selection=exclusive`
    * `:set selectmode=mouse,key`
* **设置行宽**
    * `:set textwidth=80`（设置一行显示80个字符）
    * `:set wrap`（打开自动换行，即太长的行另起一行显示）
    * `:set nowrap`（关闭自动换行）



## 永久改造

> 操作系统为Ubuntu18.04，改造前需要知道配置文件有两个：
>
> 1. 系统配置文件：`/etc/vim/vimrc`
> 2. 用户配置文件：`~/.vimrc`（home目录下本来没有`.vimrc`文件，需要用户手动创建：`vim .vimrc`）
>
> 注意，用户配置文件是优先于系统配置文件的，vim启动时会邮箱读取用户根目录下的`.vimrc`文件。综上：我们需要进行改造的是`~/.vimrc`文件。****

### 常用需求

* 显示行号
* 自动缩进
* 语法高亮
* 自动补全
* 界面美化



### 常用命令

> ***替换***

从当前行到末尾行，将 str1 全部替换为 str2 （后面加回车）

```shell
:.,$s/str1/str2/g
```



> ***跳转***

最常用的是直接跳转到某行，输入下列指令并回车：

```bash
:n
```
# SFML

## 一、SFML简介

> SFML（Simple and Fast Multimedia Library）是一个开源的基于C++的多媒体以及图形库。

【**五大模块**】

* 系统——`sfml-system.lib/sfml-system-d.lib`
* 窗口——`sfml-window.lib/sfml-window-d.lib`
* 图形——`sfml-graphics.lib/sfml-graphics-d.lib`
* 声音——`sfml-audio.lib/sfml-audio-d.lib`
* 网络——`sfml-network.lib/sfml-network-d.lib`

【**常用网站**】

* [SFML官网](https://www.sfml-dev.org/index.php)
* The [official tutorials](https://www.sfml-dev.org/tutorials/)
  * The [online API documentation](https://www.sfml-dev.org/documentation/)
  * The [community wiki](https://github.com/SFML/SFML/wiki/)
  * The [community forum](https://en.sfml-dev.org/forums/) ([French](https://fr.sfml-dev.org/forums/))

## 二、搭建SFML开发环境

* 下载安装visual studio

* 创建空项目

* 配置项目的外部头文件包含

    ![image-20220514153257526](https://gitee.com/huiba450zdy/typora-picture/raw/master/img/image-20220514153257526.png)

* 配置链接器

    ![image-20220514153732701](https://gitee.com/huiba450zdy/typora-picture/raw/master/img/image-20220514153732701.png)

* 配置debug链接文件

    ![image-20220514165538594](https://gitee.com/huiba450zdy/typora-picture/raw/master/img/image-20220514165538594.png)

* 配置debug链接文件（需要加-d，即在lib文件夹下选择动态链接文件，此处选择的是动态链接方式故加-d）

    ![image-20220514165740236](https://gitee.com/huiba450zdy/typora-picture/raw/master/img/image-20220514165740236.png)

* 复制需要的dll文件到项目路径下（动态链接需要，静态链接则不需要此步骤）

    ![image-20220514155605367](https://gitee.com/huiba450zdy/typora-picture/raw/master/img/image-20220514155605367.png)

    ![image-20220514155743402](https://gitee.com/huiba450zdy/typora-picture/raw/master/img/image-20220514155743402.png)

* 配置成功的编辑器效果：在包含SFML库的时候会自动让用户选择相关头文件

    ![image-20220514162040676](https://gitee.com/huiba450zdy/typora-picture/raw/master/img/image-20220514162040676.png)

* 运行官网用例成功

    <img src="https://gitee.com/huiba450zdy/typora-picture/raw/master/img/image-20220514170618821.png" alt="image-20220514170618821" style="zoom:50%;" />

* 配置Debug模式下输出exe可执行程序的路径，选择路径为新建项目中的\64x\Debug

    ![image-20220514172043699](https://gitee.com/huiba450zdy/typora-picture/raw/master/img/image-20220514172043699.png)

* 此时有一个问题是在项目Debug路径下直接点击生成的exe文件直接双击运行会报错：

    ![image-20220514171617222](https://gitee.com/huiba450zdy/typora-picture/raw/master/img/image-20220514171617222.png)

* 解决方法：将之前拷贝到项目路径中的dll文件再次拷贝到exe文件所在路径中去，之后即可双击运行

* 音频：无论是动态链接或者是静态链接，都需要添加`opanal.lib`到链接器依赖项中去



## 三、release版本（静态链接）

* 新建项目

* 头文件包含与之前一样

* 配置链接器

    ![image-20220514173958824](https://gitee.com/huiba450zdy/typora-picture/raw/master/img/image-20220514173958824.png)

    除此之外，还需要添加`winmm.lib`、`opengl32.lib`以及`freetype.lib`（否则会报错）。

* 配置预编译器

    ![image-20220514174145925](https://gitee.com/huiba450zdy/typora-picture/raw/master/img/image-20220514174145925.png)
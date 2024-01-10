# Mermaid in Typora

参考资料：https://mermaid-js.github.io/mermaid/#/

## 一、流程图（Flowchart）

所有的流程图都由以下几个元素构成：

* 节点（node）
* 几何图形（geometric shapes）
* 边框（edge）
* 线段和箭头（line and arrow）

mermaid语法支持几乎所有元素的自定义，以及子图（subgraph）的嵌入与关联。

> 【**注意**】节点的命名需要首字母大写或者全拼大写（“End”或“END”），否则可能造成构图失败



### 1.1 节点（Node）

节点可以理解为边框（edge）和文本（显示在边框中的内容）的组合，下图中文本是`Id`边框是实线矩形：

```mermaid
flowchart LR
    Id
```

#### 1.1.1 自定义边框

自定义边框是在初始文本后面跟一些组合符号，组合符号内加上最终文本（会覆盖初始文本）。在这里初始文本都以`id1`为例，最终文本为边框形状。

* 圆角矩形（round edges）

    ```mermaid
    flowchart LR
        id1(round edge)
    ```

* 体育场形（stadium-shaped）

    ```mermaid
    flowchart LR
        id1([stadium-shaped])
    ```

* 子程序形（subroutine shape）

    ```mermaid
    flowchart LR
        id1[[subroutine shape]]
    ```

    

* 圆柱形（cylindrical）

    ```mermaid
    flowchart LR
        id1[(cylinder)]
    ```

* 圆形（circle）

    ```mermaid
    flowchart LR
        id1((circle))
    ```

* 不对称形状（asymmetric）

    ```mermaid
    flowchart LR
        id1>asymmetric]
    ```

* 菱形（rhombus）

    ```mermaid
    flowchart TB
        id1{rhombus}
    ```

* 六边形（hexagon）

    ```mermaid
    flowchart LR
        id1{{hexagon}}
    ```

* 平行四边形（parallelogram）

    ```mermaid
    flowchart TB
        id1[/parallelogram/]
    ```

* 反平行四边形（parallelogram alt）

    ```mermaid
    flowchart TB
        id1[\parallelogram alt\]
    ```

* 梯形（Trapezoid）

    ```mermaid
    flowchart TB
        id1[/Trapezoid\]
    ```

* 倒梯形（Trapezoid alt）

    ```mermaid
    flowchart TB
        id1[\Trapezoid alt/]
    ```

* 圆环形（Double circle）

    由于版本原因，暂时无法回绘制。

    

### 1.2 图方向（Graph）

确定图的方向，需要声明是自顶向下`TB`还是自底向上`BT`

```mermaid
flowchart TB
    Start --> Stop
```

自左向右`LR`

```mermaid
flowchart LR
    Start --> Stop
```

图方向汇总：

* `TD`：自上而下（同TB）
* `TB`：自顶向下
* `BT`：自底向上
* `LR`：从左往右
* `RL`：从右往左



### 1.3 连接线（Links）

节点之间可以通过线（link）或者边（edge）来连接

#### 1.3.1 实线

```mermaid
flowchart LR
    A --- B
```

#### 1.3.2 带箭头实线

```mermaid
flowchart LR
    A <--> B
```

#### 1.3.3 带文本实线

* 不带箭头

    方法一：

```mermaid
flowchart LR
   A -- text --- B
```

​        方法二：

```mermaid
flowchart LR
   A ---|test| B
```

* 带箭头

    方法一：

    ```mermaid
    flowchart LR
        A -- text --> B
    ```

    方法二：

    ```mermaid
    flowchart LR
        A -->|test| B
    ```

#### 1.3.4 带箭头虚线

```mermaid
flowchart LR
    A -.-> B
```

#### 1.3.5 带文本虚线

```merimaid
flowchart LR
    A-. text .->B
```

#### 1.3.6 粗实线

```mermaid
flowchart LR
    A ==> B
```

带文本：

```mermaid
flowchart LR
    A == text ==> B
```

#### 1.3.7 链式连接

不带文本：

```mermaid
flowchart LR
    A --> B --> C
```

带文本：

```mermaid
flowchart LR
    A -- text1 --> B -- text2 --> C
```

平行链路：

```mermaid
flowchart LR
    A --> B & C -->D
```

交叉链路：

```mermaid
flowchart LR
    A & B --> C & D
```



### 1.4 指定连接长度

```mermaid
flowchart TB
    A([Start]) --> B{Is it?}
    B -->|Yes| C[OK]
    C --> D[Rethink]
    D --> B
    B ---->|No| E([End])
```

> 在`B`到`E`的连接语句中，额外指定了两个短横线`--`，这样就会跳过默认长度的两级（rank）

常用线形与级数长度对照如下：

![image-20220914171101329](https://raw.githubusercontent.com/huibazdy/TyporaPicture/main/202209141711371.png)



### 1.5 子图（Subgraph）

添加子图格式如下：

```
subgraph title
    graph definition
end
```

【例子】

```mermaid
flowchart TB
    subgraph graph1[one]
    a1 --> a2
    end
    
    subgraph graph2
    b1 --> b2
    end
    
    subgraph graph3
    c1 --> c2
    end
    
    c1 --> a2
```

【子图和子图的边也可以连接】

```mermaid
flowchart TB
    subgraph one
    a1 --> a2
    end
    
    subgraph two
    b1 --> b2
    end
    
    subgraph three
    c1 --> c2
    end
    
    c1 --> a2
    one --> two
    three --> two
    two --> c2
```

【子图方向】

```mermaid
flowchart LR
    subgraph TOP
      direction TB
      subgraph B1
        direction RL
        i1 --> f2
      end
      subgraph B2
        direction BT
        i2 --> f2
      end
    end
    
    A --> TOP --> B
    B1 --> B2
```



### 1.6 TCP/IP网络协议栈实战

```mermaid
flowchart TB
    subgraph application  %%应用层
      direction LR
      subgraph DNS
      end
      subgraph HTTP
      end
      subgraph HTTPS
      end
    end
    
    subgraph tansmission
      direction LR
      subgraph TCP
      end
      subgraph UDP
      end
    end
    
    subgraph Internet
      direction LR
      subgraph ICMP
      end
      subgraph IP
      end
      subgraph IGMP
      end
    end
    
    subgraph Linker
      direction TB
      subgraph ARP
      end
      subgraph Ethernet
      end
      subgraph WIFI
      end
      ARP --> Ethernet
    end
    
    subgraph Router
    end
    
    HTTP -.-> TCP
    TCP -.-> IP
    IP -.-> ARP
    Ethernet -.-> Router
```




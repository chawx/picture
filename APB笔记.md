# APB笔记

有两个周期 

第一个周期 地址 数据

第二周期 数据写进地址 或者根据地址读取数据



有一个Bridge



Advanced Peripheral Bus

低功耗接口简单控制简单

低俗功耗低的外围

![](https://raw.githubusercontent.com/chawx/picture/main/imageSnipaste_2024-02-20_17-05-13.png)

APB = APB bridge master+ 外围 slave



好多信号

PCLK clock

Ret

Add 32 bits wide

Psel master slave 连接信号

PENABLE 标志进入了阶段

PWRITE 标志写入数据 还是 读取数据

PREADY  1 表明数据接收完成

PRDATA  



Address bus

Data bus



Transfer

分为写传输和读传输 有等待无等待

![](https://raw.githubusercontent.com/chawx/picture/main/imageSnipaste_2024-02-20_17-06-56.png)

写操作 没有等待：

set up 阶段 access phase数据传输阶段

检测pready信号为1 表示传输完成

信号是通过bridge发送过来的

电容充放电 经过一段时间才会让信号发生改变

![](https://raw.githubusercontent.com/chawx/picture/main/imageSnipaste_2024-02-20_17-07-23.png)

写操作 有等待：

不一样时刻pready 等待了一段时间 才变为1

拉低pready信号可以让传输延长两个周期



读操作 无等待：

相同的与写操作 pwrite变为0

![](https://raw.githubusercontent.com/chawx/picture/main/imageSnipaste_2024-02-20_17-07-54.png)

error

psalverr

protection unit supprot



状态机：

问题：

从主机的角度看待问题 实际上写代码从从机的角度看问题

信号转变条件很不明确 transfer master 传输数据意愿很抽象 关系到master是不是想要传输数据 

![](https://raw.githubusercontent.com/chawx/picture/main/imageSnipaste_2024-02-20_17-08-41.png)

改动一下，从slave角度

![](https://raw.githubusercontent.com/chawx/picture/main/imageSnipaste_2024-02-20_17-09-07.png)

没有ready信号，本身是slave发出的信号，不会根据自己的信号判断自己的状态



APB总线协议的说明



用代码和模块来表述一下APB总线协议

![](https://raw.githubusercontent.com/chawx/picture/main/imageSnipaste_2024-02-20_17-09-40.png)

slave没有很多接口 不会发出一些ready response 信号 
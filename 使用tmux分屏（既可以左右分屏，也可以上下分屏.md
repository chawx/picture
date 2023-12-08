# 使用tmux分屏（既可以左右分屏，也可以上下分屏

### （1）安装工具

在ubuntu系统中使用sudo apt-get install tmux安装tmux工具

### （2）使用工具

1. `输入命令tmux使用工具`
2. `上下分屏：ctrl + b 再按 "`
3. `左右分屏：ctrl + b 再按 %`
4. `切换屏幕：ctrl + b 再按o`
5. `关闭一个终端：ctrl + b 再按x`
6. `上下分屏与左右分屏切换： ctrl + b 再按空格键`
7. `exit为退出tmux`
8. `切换端口：ctrl + b 再按N`
9. `'CTRL-b z` ：使窗格全屏显示。再次点击 `CTRL-b z` 以将其缩小到之前的大小

## 终端分屏tmux

### 分屏效果

 tmux并不是一个类似bash的终端，而是管理在管理会话，使用tmux后，其他配置还是和bash或zsh一样。

效果如图：

![](https://raw.githubusercontent.com/chawx/picture/main/imageSnipaste_2023-11-26_16-17-55.png)

## tmux的基本命令

在bash或zsh中输入tmux打开新的会话。**可以配置在bash后zsh的配置文件中，启动bash自动运行tmux命令**

**默认前缀ctrl+b（命令中替换prefix）**

tmux中，使用分割窗格等需要使用快捷键。使用每个快捷键前，会先键入前缀， 使得tmux开始监听后面的命令。没有键入前缀，直接使用命令是不会触发tmux。

目前经常使用：

**会话：**每次断开连接没有关闭tmux，再次连接的时候，运行tmux命令会新建一个会话。当进入bash后，使用tmux ls可以查看后台未关闭的会话。进入会话后，可以使用快捷键，列出存在的会话。

| 会话命令                       | 作用                               |
| ------------------------------ | ---------------------------------- |
| **tmux ls**                    | **显示所有的会话**                 |
| **tmux kill-session -t s1**    | **关闭会话s1**                     |
| **tmux kill-session -a -t s1** | **关闭除s1外的所有会话**           |
| **tmux kill-server**           | **关闭所有会话**                   |
| **prefix s**                   | **在会话中，列出会话，可进行切换** |

**窗格：**每个窗口可以显示多个窗格

| 窗格命令                      | 作用                             |
| ----------------------------- | -------------------------------- |
| **prefix %**                  | **水平方向创建窗格**             |
| **prefix "**                  | **垂直方向创建窗格**             |
| **prefix Up,Down,Left,Right** | **根据箭头方向切换窗格**         |
| **prefix }{**                 | **与下上一个窗格交换位置**       |
| **prefix x**                  | **关闭当前窗格**                 |
| **prefix space(空格键)**      | **重新排列当前窗口下的所有窗格** |

**窗口：**每个会话，可以包含多个窗口。

| 窗口命令       | 作用                         |
| -------------- | :--------------------------- |
| **prefix c**   | **创建一个新窗口**           |
| **prefix w**   | **列出所有窗口，可进行切换** |
| **prefix np**  | **进入下上一个窗口**         |
| **prefix 0~9** | **选择编号0~9对应的窗口**    |
| **prefix &**   | **关闭当前窗口**             |





## ****常用命令\****

**tmux new**　　创建默认名称的会话（在tmux命令模式使用**new**命令可实现同样的功能，其他命令同理，后文不再列出tmux终端命令）

**tmux new -s mysession**　　创建名为mysession的会话

**tmux ls**　　显示会话列表

**tmux a**　　连接上一个会话

**tmux a -t mysession**　　连接指定会话

**tmux rename -t s1 s2**　　重命名会话s1为s2

**tmux kill-session**　　关闭上次打开的会话

**tmux kill-session -t s1**　　关闭会话s1

**tmux kill-session -a -t s1**　　关闭除s1外的所有会话

**tmux kill-server**　　关闭所有会话

**常用快捷键**
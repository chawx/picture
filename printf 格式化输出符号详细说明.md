# printf 格式化输出符号详细说明

%a  浮点数、十六进制数字和p-记数法（c99
%A  浮点数、十六进制数字和p-记法（c99）
%c  一个字符(char)
%C  一个ISO宽字符
%d  有符号十进制整数(int)（%ld、%Ld：长整型数据(long),%hd：输出短整形。）　
%e  浮点数、e-记数法
%E  浮点数、E-记数法
%f  单精度浮点数(默认float)、十进制记数法（%.nf  这里n表示精确到小数位后n位.十进制计数）
%g  根据数值不同自动选择%f或%e．
%G  根据数值不同自动选择%f或%e.
%i  有符号十进制数（与%d相同）
%o  无符号八进制整数
%p  指针
%s  对应字符串char*（%s = %hs = %hS 输出 窄字符）
%S  对应宽字符串WCAHR*（%ws = %S 输出宽字符串）
%u  无符号十进制整数(unsigned int)
%x  使用十六进制数字0xf的无符号十六进制整数　
%X  使用十六进制数字0xf的无符号十六进制整数
%%  打印一个百分号

%I64d 用于INT64 或者 long long
%I64u 用于UINT64 或者 unsigned long long
%I64x 用于64位16进制数据

![](https://raw.githubusercontent.com/chawx/picture/main/imageSnipaste_2023-11-29_22-07-02.png)
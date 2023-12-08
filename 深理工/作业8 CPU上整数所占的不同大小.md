# 作业8 CPU上整数所占的不同大小

（1） 64位机器

Size of char is:          1
Size of unsigned char is:      1
Size of [signed](https://so.csdn.net/so/search?q=signed&spm=1001.2101.3001.7020) char is:       1
Size of int is:           4
Size of short is:          2
Size of long is:          8
Size of long int is:         8
Size of signed int is:       4
Size of unsigned int is:      4
Size of unsigned long int is:   8
Size of long long int is:     8
Size of unsigned long long is:    8
Size of float is:         4
Size of double is:         8
Size of long double is:     16
任何数据类型的指针都是占8个字节

（2）32位机器上
Size of char is:           1
Size of unsigned char is:      1
Size of signed char is:       1
Size of int is:            4
Size of short is:          2
Size of long is:           4
Size of long int is:        4
Size of signed int is:       4
Size of unsigned int is:     4
Size of unsigned long int is:     4
Size of long long int is:        8
Size of unsigned long long is:    8
Size of float is:          4
Size of double is:         8
Size of long double is:     8

任何数据类型的指针都是占4个字节

（3）16位平台

char     1个字节8位
short    2个字节16位
int      2个字节16位
long     4个字节32位
指针     2个字节
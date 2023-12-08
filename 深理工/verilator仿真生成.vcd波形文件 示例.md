# verilator仿真生成.vcd波形文件 示例

### 1、模块准备

首先，我们先写好一个模块，如our_OnOff.v:

```verilog
module our_OnOff(
    input a,
    input b,
    output f
);
  assign f = a ^ b;

endmodule
```

### 2、测试模块

main.cpp 如下：

```cpp
#include <stdio.h>
#include <stdlib.h>
#include <assert.h>
#include "Vour_OnOff.h"
#include "verilated_vcd_c.h"

vluint64_t main_time = 0;  //initial 仿真时间

double sc_time_stamp()
 {
     return main_time;
 }


int main(int argc,char **argv)
{
     Verilated::commandArgs(argc,argv);
	 Verilated::traceEverOn(true); //导出vcd波形需要加此语句
     VerilatedVcdC* tfp = new VerilatedVcdC(); //导出vcd波形需要加此语句
     Vour_OnOff *top = new Vour_OnOff("top");
	 top->trace(tfp, 0);
     tfp->open("wave.vcd"); //打开vcd
      while(!sc_time_stamp() < 20 && !Verilated::gotFinish())
     {                                                 
     int a = rand() & 1;
     int b = rand() & 1;
     top->b = b;
     top->eval();
     printf("a = %d, b = %d, f = %d\n",a,b, top->f);
     tfp->dump(main_time); //dump wave
     main_time++; //推动仿真时间
     }
     top->final();
     tfp->close();
     delete top;
     return 0;
}
```

在一次循环中, 代码将会随机生成两个1比特信号, 用来驱动两个输入端口, 然后通过`eval()`函数更新电路的状态, 这样我们就可以读取输出端口的值并打印. 为了自动检查结果是否正确, 我们通过`assert()`语句对输出结果进行检查.

### 3、运行仿真

运行仿真分成三步：

#### a、生成目标文件夹

```bash
verilator -Wall --cc --exe --build main.cpp our_OnOff.v --trace
```

 **b、编译**

```bash
make -C obj_dir -f Vour_OnOff.mk Vour_OnOff
```

#### c、运行

```bash
./obj_dir/Vour_OnOff
```

d、运行波形

```shell
gtkwave wave.vcd 
```



安装sudo aptitude
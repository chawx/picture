# 搭建verilator仿真环境

## 下面是搭建verilator环境

[【一生一芯】搭建verilator仿真环境 - 老吴家的小阿哲 - 博客园 (cnblogs.com)](https://www.cnblogs.com/Wishengine/p/17447398.html)



## 看verilator手册总结

```verilog
module our;
	initial begin 
	$display("Hello World");
 	$finish; 
end
endmodule
```

现在，我们在小示例上运行Verilator

```cmake
verilator --binary -j 0 -Wall our.v
```

分解此命令：

1.--binary 告诉 Verilator 完成创建模拟可执行文件所需的一切。

2.-j 0 使用与计算机拥有的 CPU 线程数一样多的 CPU 线程进行验证。

3.-Wall 因此 Verilator 启用了更强的 lint 警告。

4.最后是our.v，这是我们的SystemVerilog设计文件。

现在我们运行它：

```
obj_dir/Vour
```



```c++
#include "Vour.h"
#include "verilated.h"
    int main(int argc, char** argv) {
    VerilatedContext* contextp = new VerilatedContext;
    contextp->commandArgs(argc, argv);
    Vour* top = new Vour{contextp};
    while (!contextp->gotFinish()) { 
    	top->eval(); 
    }
    delete top;
    delete contextp;
    return 0;
}
```



```cmake
verilator --cc --exe --build -j 0 -Wall sim_main.cpp our.v
```

分解此命令

1、--cc 获取 C++ 输出（与 SystemC 或仅 linting 相比）。

2、--exe，以及我们的sim_main.cpp包装文件，因此构建将创建一个可执行文件，而不仅仅是一个库。

3、--build，以便 Verilator 调用 make itself。也就是说，我们不需要手动调用 make 作为单独的步骤。您还可以编写自己的编译规则，并运行 make yourself，如示例 SystemC 执行中所示。

4、-j 0 使用与计算机拥有的 CPU 线程数一样多的 CPU 线程进行验证。

5.-Wall so Verilator has stronger lint warnings enabled.



## Verilator将使用--cc选项将SystemVerilog设计转换为C++，或使用--sc选项转换为SystemC
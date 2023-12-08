## Makefile（Nvboard）

```makefile
TOPNAME = top
NXDC_FILES = constr/top.nxdc
INC_PATH ?=

VERILATOR = verilator
VERILATOR_CFLAGS += -MMD --build -cc  \
				-O3 --x-assign fast --x-initial fast --noassert

BUILD_DIR = ./build
OBJ_DIR = $(BUILD_DIR)/obj_dir
BIN = $(BUILD_DIR)/$(TOPNAME)

default: $(BIN)

$(shell mkdir -p $(BUILD_DIR))

# constraint file
SRC_AUTO_BIND = $(abspath $(BUILD_DIR)/auto_bind.cpp)
$(SRC_AUTO_BIND): $(NXDC_FILES)
	python3 $(NVBOARD_HOME)/scripts/auto_pin_bind.py $^ $@

# project source
VSRCS = $(shell find $(abspath ./vsrc) -name "*.v")
CSRCS = $(shell find $(abspath ./csrc) -name "*.c" -or -name "*.cc" -or -name "*.cpp")
CSRCS += $(SRC_AUTO_BIND)

# rules for NVBoard
include $(NVBOARD_HOME)/scripts/nvboard.mk

# rules for verilator
INCFLAGS = $(addprefix -I, $(INC_PATH))
CXXFLAGS += $(INCFLAGS) -DTOP_NAME="\"V$(TOPNAME)\""

$(BIN): $(VSRCS) $(CSRCS) $(NVBOARD_ARCHIVE)
	@rm -rf $(OBJ_DIR)
	$(VERILATOR) $(VERILATOR_CFLAGS) \
		--top-module $(TOPNAME) $^ \
		$(addprefix -CFLAGS , $(CXXFLAGS)) $(addprefix -LDFLAGS , $(LDFLAGS)) \
		--Mdir $(OBJ_DIR) --exe -o $(abspath $(BIN))

all: default

run: $(BIN)
	@$^

clean:
	rm -rf $(BUILD_DIR)

.PHONY: default all clean run
```

```makefile
BIN = $(BUILD_DIR)/$(TOPNAME)
```

在Makefile中，BIN = $(BUILD_DIR)/$(TOPNAME) 是一个变量定义语句。它定义了一个名为BIN的变量，其值是由BUILD_DIR和TOPNAME两个变量拼接而成。

具体来说，BUILD_DIR是一个目录路径，TOPNAME是顶层模块的名称。通过将它们拼接在一起，就得到了完整的可执行文件的路径。

例如，如果BUILD_DIR的值是./build，TOPNAME的值是top，那么BIN的值将是./build/top，表示生成的可执行文件的路径为"./build/top"。

```makefile
$(shell mkdir -p $(BUILD_DIR))
```

`$(shell mkdir -p $(BUILD_DIR))` 

是Makefile中的一个命令执行语句。它用于创建目录。

在这里，`mkdir -p $(BUILD_DIR)` 是一个shell命令，用于创建目录。`-p`选项表示递归创建目录，即如果父目录不存在，也会一并创建。

`$(shell ...)` 是Makefile中的命令执行语法，用于执行shell命令并获取其输出结果。

```Makefile
$(SRC_AUTO_BIND): $(NXDC_FILES)

python3 $(NVBOARD_HOME)/scripts/auto_pin_bind.py $^ $@
```

这是一个规则，用于生成文件 `$(SRC_AUTO_BIND)`。它指定了依赖关系，即 `$(SRC_AUTO_BIND)` 依赖于 `$(NXDC_FILES)`。

在规则的命令部分，使用 `python3` 命令执行脚本 `$(NVBOARD_HOME)/scripts/auto_pin_bind.py`。它接受两个参数：`$^` 和 `$@`。这两个变量是自动化变量，具体含义如下：

- `$^` 表示所有的依赖文件，即 `$(NXDC_FILES)`。
- `$@` 表示目标文件，即 `$(SRC_AUTO_BIND)`。

```Makefile
VSRCS = $(shell find $(abspath ./vsrc) -name ".v")

CSRCS = $(shell find $(abspath ./csrc) -name ".c" -or -name ".cc" -or -name ".cpp")

CSRCS += $(SRC_AUTO_BIND)
```

这段代码定义了两个变量 VSRCS 和 CSRCS，用于存储项目的源文件。

VSRCS 变量使用 find 命令查找路径 $(abspath ./vsrc) 下所有以 .v 结尾的文件，并将结果赋值给 VSRCS。
CSRCS 变量使用 find 命令查找路径 $(abspath ./csrc) 下所有以 .c、.cc 或 .cpp 结尾的文件，并将结果赋值给 CSRCS。
然后，通过 += 运算符将 $(SRC_AUTO_BIND) 添加到 CSRCS 变量中，以确保自动生成的文件也包含在编译过程中。
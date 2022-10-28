#### 函数指针

---

#### burn craneG:

- Use the compiled code in gerrrit, for the code in ubuntu cannot download in PC.
- Run sscom.exe and press RESET buttton, then you can see the version.Replace the old file with the new file in version folder.
- Run Aboot.exe and click Release dashboard, choose the correspond chip, click Release button. After release finished, click the Download button. Specially, press the RESET button and the DOWNLOAD button in DKB and the chip will enter burn program mode.
- Note: You can read the log output of sscom to check the code.

---

#### git command:

```git
git checkout . : back file to workspace
git status -s  : view the file information  
```

---

#### cd command:

```linux
cd /        : root 
cd ~        : home
cd -        : return to before dir when enter this dir.
cd ..       : return to the previous dir.
cd ../..    : return to the dir before previous dir.
```

---

#### vim complier:

- commamd mode : use i, a, o etc to enter input mode. ues '': ' to enter the last line mode.
- input mode : edit
- the last line mode : use q, w etc to quit the vim. **Note** the ESC can quit this mode anytime.

---

#### typedef :

```c
typedef unsigned int UINT; //replace UINT to int, the later replace the former

typedef struct Count{
   int x;
   int y;
   int c;
}NUM;    //NUM replace Count various.

typedef struct Count{
   struct Count *p_Count;  //struct Count donot omit.
}*pC;  //define struct Count point *pC
```

---

#### Function Pointer

```c
int (*p)(int, int ) //The later brackets are parameters. 
//The later brackets are parameters. The * is return value.
```

---

#### RISCV约定的寄存器分配

| 寄存器     | 汇编名称   | 功能描述                        |
| ------- | ------ | --------------------------- |
| x0      | zero   | 零寄存器                        |
| x1      | ra     | 返回地址                        |
| x2      | sp     | 栈指针                         |
| x3      | gp     | 全局指针                        |
| x4      | tp     | 线程指针                        |
| x5      | t0     | 临时寄存器，或者用作替代链接寄存器           |
| x6      | t1     | 临时寄存器                       |
| x7      | t2     | 临时寄存器                       |
| x8      | s0/fp  | 该寄存器需要被调函数予以保存，或也可用作调用栈的帧指针 |
| x9      | s1     | 该寄存器需要被调函数予以保存              |
| x10~x11 | a0~ a1 | 函数参数或返回值                    |
| x12~x17 | a2~a7  | 函数参数                        |
| x18~x27 | s2~s11 | 该寄存器需要被调函数予以保存              |
| x28~x31 | t3~t6  | 临时寄存器                       |

---

#### RISC-V assembly instruction

```nasm
csrr mstatus 0x80        ;enable interrupt  
csrr mstatus 0x00        ;disable interrupt
```

---

#### 书写Makefile总结：

1. Makefile中PROJECT名称要跟该项目下的.c文件相同

2. Makefile中管道符-->`|`
   
   有时，需要定义一个这样的规则，在更新目标（ 目标文件已经存在）时只需要根据依赖文件中的部分来决定目标是否需要被重建，而不是在依赖文件的任何一个被修改后都重建目标。为了实现这一目的，相应的就需要对规则的依赖进行分类，一类是在这些依赖文件被更新后，需要更新规则的目标；另一类是更新这些依赖的，可不需要更新规则的目标。我们把第二类称为：“ order-only”依赖。书写规则时，“ order-only”依赖使用管道符号“ |”开始，作为目标的一个依赖文件。规则依赖列表中管道符号“ |”左边的是常规依赖，管道符号右边的就是“ order-only”依赖。这样的规则书写格式如下：  
   TARGETS : NORMAL-PREREQUISITES | ORDER-ONLY-PREREQUISITES
   
   - $(Q) 变量的本质就是 Makefile中的命令显示与否
   
   - |grep就是指把上个命令运行的结果通过管道命令带入到grep的参数里执行，
     所以单纯的grep没什么意义，一般使用都是通过管道符来使用grep
   
   -  -*v* 表示反向选择 "*^\s*#*" 表示匹配以S开头的字符串
   
   - (\s*)表示连续空格的字符串

3. 在Makefile中的include要记得看路径是否正确，为了方便都是使用宏来代替的，记得要查看宏的定义，每个人定义方式不同

4. make命令可以显式定义DEFINES，为c预处理设定任意的变量：**make TARGET=esb DEFINES=MYTRACE,MYVALUE=4711**
   
   还可以保存默认的DEFINES到**Makefile.$(TARGET).DEFINES**中：**make TARGET=esb DEFINES=MYTRACE,MYVALUE=4711 savedefines**

5. 通过变量“ VPATH”可以指定依赖文件的搜索路径

6. 在Makefile中输出信息：`$(info information)`

---

#### Makefile 函数：

```makefile
$(strip <string> )
#去掉<string>字串中开头和结尾的空字符,包括 空格, tab 等不可显示的字符
#并将中间的多个连续空字符(如果有的话)合并为一个空字符

$(wildcard PATTERN...)
#展开为已经存在的、使用空格分开的、匹配此模式的所有文件列表
#如果不存在任何符合此模式的文件，函数会忽略模式字符并返回空

$(words TEXT)
#计算字符串“ TEXT”中单词的数目
#返回“ TEXT”字串中的单词数

$(filter PATTERN…,TEXT)
#过滤函数— filter,过滤掉字串“ TEXT”中所有不符合模式“PATTERN”的单词
#返回所有符合此模式的单词

$(call FUNCTION)
 #call”函数可以实现对用户自己定义函数引用


$(addprefix PREFIX,NAMES…)
#加前缀函数— addprefix

$(shell syntax)
#函数“ shell”所实现的功能和shell中的引用（ ``）相同，实现对命令的扩展


$(info information)
#在Makefile中实时输出信息
```
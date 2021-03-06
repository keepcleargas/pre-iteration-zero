# 技术选型

2011年，我们项目组在开发一个给公司内部使用的`IDE`，这个IDE是一个典型的C/S结构的软件，客户端使用VC编写，服务器端则运行在`Linux`上，所有的编译，链接，模拟运行等都在服务器上，客户端只提供一个简单的文本编辑器。

客户端与服务器通过一系列的服务来通信，这些服务有点像当时比较流行的SOAP方式，但是又不完全是（比如没有服务发现）。比如`创建文件`，`编译模块`，`测试模块`都是不同的服务。客户端通过HTTP来调用这些不同的服务，来提供完整的功能。

截止目前，听起来还挺正常吧？问题是，后台使用了C作为主要编程语言，数据库访问使用Oracle提供的ProC（那确实是个灾难，你应该可以想象在C语言中嵌入那些奇形怪状的预处理代码有多恶心），再往后是TUXEDO中间件。

```c
//这个例子来自Oracle ProC官方网站
//http://docs.oracle.com/cd/E11882_01/appdev.112/e10825/pc_08arr.htm#g20885

int   emp_number[20]; 
float salary[20]; 
 
EXEC SQL DECLARE emp_cursor CURSOR FOR 
    SELECT empno, sal FROM emp; 
 
EXEC SQL OPEN emp_cursor; 
 
EXEC SQL WHENEVER NOT FOUND do break; 
for (;;) 
{ 
    EXEC SQL FETCH emp_cursor 
        INTO :emp_number, :salary; 
    /* process batch of rows */ 
    ... 
} 
...
```

我们项目中有6个开发，3个测试，项目进行了差不多1年，仍然没有一个比较稳定的版本。后来部门决定换掉那个老旧的`TUXEDO`，换成另一个自己写的用C语言编写的中间件。这个工具后来在深圳分公司做试点，但是依旧不是很稳定。通过这个IDE开发出来的服务很难调试，我们不得不将对`gdb`进行了部分封装，然后尝试使用`netbeans`协议来做远程的debug，不过过程中发现这种机制需要编写很多代码，而且这部分代码则更加难以调试。

一个折中的办法是让开发通过`ssh`远程登录到服务器上，用`gdb`attach到对应的进程上进行调试。不过这个由于IDE的设计初衷相违背（这个IDE的目的是降低服务的开发难度而不是增加）。印象中，在我离开那个项目之前，这个问题都没有得到很好的解决。

这是一个典型的，被技术选型害了的场景。如果我们使用更易于开发，调试，维护的Java平台，或者动态语言如Ruby，Python，开发周期至少可以缩短一半。至于设计时考虑的那些性能问题，其实很可能并不是真正的问题，我们并不需要支持数万人同时在线，也无需考虑超大规模的数据库备份方案，毕竟当时整个公司的开发也不过200人。

我们选择了错误的编程语言，错误的数据库模型，错误的软件架构，实现了一个没有太多人使用的"产品"。其实归纳起来，成语`方枘圆凿`可以很传神的描述我们做的事情。


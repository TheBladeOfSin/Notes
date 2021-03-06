## **Java**简介
### 概述  
> Java是一门<font color=red>**面向对象**</font>编程语言，
> 是作为静态面向对象编程语言的代表，极好地实现了面向对象理论。

### **Java**体系结构

* Java编程语言
* 字节码
* <font color=yellow>Java API</font>
* <font color=yellow>JVM（Java虚拟机）</font>

> * ####  编译过程 
>
> > Java编程语言          --编写源代码 -->  
> > Java前端编译器       --编译为**字节码** -->  
> > Java虚拟机（JVM） --解释/编译为机器指令运行  
> >
> > ![](https://raw.githubusercontent.com/TheBladeOfSin/Image/Learning-Library/Img/JavaCompilationProcess.png)
> >
> ---
>
> * #### **字节码：** 
> > 编程语言的编译结果满足并包含Java虚拟机的内部指令集、符号表以及一些其他辅助信息的话，这个编译结果就是一个有效的字节码文件。  
> > 
> > * #### <font color=green>**[ 字节码作用 ]：**</font> 为Java跨平台提供了支持。正是因为源代码编译后为字节码文件，而字节码文件相较机器指令,字节码可以解决程序的安全性问题、跨平台移植性问题。而且源码只需一次编译，得到的字节码文件可以在不同的平台上运行。
>
> ---
> * #### <font color=yellow>**Java API：**</font> 
>> 预先定义的接口，目的是提供应用程序与开发人员基于某软件或硬件的以访问一组例程的能力，而又不需要访问源码或者理解内部工作机制的细节。 
>> 
>> * <font color=green>**[ Java API作用 ]：**</font> 支持平台无关性和安全性使得Java程序适应任何应用程序  
> ---
> <font color=yellow>**JVM（Java虚拟机）：**</font> 
>
> > 其主要任务为将字节码装载到内部，解释/编译为对应平台上的机器指令执行
> >
> >  
> > Java跨平台支持--JVM：![Java跨平台支持--JVM](https://raw.githubusercontent.com/TheBladeOfSin/Image/Learning-Library/Img/JavaCross-Platform(JVM).png)


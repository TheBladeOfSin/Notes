## 数据类型
### 八种基本类型

> *  ### 六种数字类型（四个整数型，两个浮点型）
> > <font color=red>**byte** </font>、**short** 、<font color=red>**int**</font>  、**long** 、<font color=red>**float**</font> 、<font color=red>**double** </font>
> >
> > 1. **<font color=red>byte</font>、short、<font color=red>int</font>、long： **  都是有符号，以二进制补码表示的整数。
> >    该三个变量所占空间分别为：1字节、2字节、3字节、6字节。
> >    
> >    ​			   二进制位数分别为：8位、16位、32位、64位。
> > - byte常用在大型数组中节约空间。
> >   
> > - Short 数据类型也可以节省空间。一个short变量是int型变量所占空间的二分之一（不常用）。
> >   
> > - 一般地整型变量默认为 int 类型。
> >   
> > - long主要使用在需要比较大整数的系统上。
> >   
> > 2. <font color=red>**float** 、**double：**</font>符合IEEE 754标准的浮点数。
> >     两者都无法表示精确的值。
> > * float为单精度、二进制位数为32位。
> > * double为双精度、二进制位数为64位。
> > ---
> * ### 字符类型
> > **char：** 单一的 16 位 Unicode 字符
> > --- 
> > char 数据类型可以储存任何单个字符。
> >
> > ---
>
> * 布尔型
> > **boolean：** 数据类型表示1位的信息。
> > 该类型只作为一种标志来记录 true/false 情况。
> >
> > --- 
>
> 不同数据类型的默认值：
> | <font color=red>**数据类型**</font> | <font color=red>**默认值**</font> |
> | :-------: | :--------: |
> | byte | 0 |
> | short |                 0                 |
> |                 int                 |                 0                 |
> |                long                 |                0L                 |
> |                float                | 0.0f |
> |               double                | 0.0d |
> |                char                 | 'u0000' |
> |               boolean               | false |
>
> 
>
> ---
### 引用类型

> 引用类型指向一个对象，指向对象的变量是引用变量。
>
> 

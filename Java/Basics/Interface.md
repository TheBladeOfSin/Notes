## 接口

### 概述  

> 在JAVA编程语言中是一个抽象类型，是抽象方法的集合。
> 一个类通过继承接口的方式，从而来继承接口的抽象方法。
>
> 关键字：<font color=red>**interface**</font>

### 划分点

* 接口的声明
* 接口特性
* 接口的继承与实现

> * ####  接口的声明
>
> > 修饰词 interface 接口名称 [extends 其他的接口名] {
> >   		//抽象方法
>   }
>
>   ```  java
>   public interface InterfaceName {
>       public void run();
>   }
>   
>   ```
>
>   
>
>
> ---
>
> * #### 接口特性
>
> > * 接口中每一个方法也是隐式抽象的,接口中的方法会被隐式的指定为 **public abstract** （其他修饰符都会报错）
> >* 接口中可以含有变量，但是接口中的变量会被隐式的指定为 **public static final** 变量（并且只能是 public）
> > * 接口中的方法是不能在接口中实现的，只能由实现接口的类来实现接口中的方法。
> >
>
> ---
>
> * 接口的继承与实现
>
> > a
> >
> 
> **<font color=red>接口的存在也是为了弥补类无法多继承的缺点</font>**

<font color=red></font>
<font color=yellow></font>
<font color=green></font>
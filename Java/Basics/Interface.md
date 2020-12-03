## 接口

### 概述  

> 在JAVA编程语言中是一个抽象类型，是抽象方法的集合。
> 一个类通过继承接口的方式，从而来继承接口的抽象方法。
>
> 关键字：<font color=red>**interface**</font>
>			  <font color=red>**implments**</font>

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
> > * 接口中每一个方法也是<font color=red>隐式抽象</font>的,接口中的方法会被隐式的指定为 <font color=yellow>**public abstract** （其他修饰符都会报错）</font>
> >* 接口中可以含有变量，但是接口中的变量会被隐式的指定为<font color=yellow> **public static final** 变量（并且只能是 public）</font>
> > * 接口中的方法是不能在接口中实现的，只能由实现接口的类来实现接口中的方法。
> >
>
> ---
>
> * 接口的继承与实现
>
> > 当类实现接口的时候，类要实现接口中所有的方法。<font color=yellow>否则，类必须声明为抽象的类</font>
> >
> > 一个接口能继承另一个接口，和类之间的继承方式比较相似。接口的继承使用<font color=red>extends</font>关键字，子接口继承父接口的方法。
> > <font color=yellow>在Java中，类的多继承是不合法，但接口允许多继承。</font>接口实现可以变相地使java具有多继承的特性。
> > 在接口的多继承中extends关键字只需要使用一次，在其后跟着继承接口。
> >
> > ``` java
> > public interface InterfaceName extends Father1, Father2{
> >     	public void run();
> > }
> > ```
> >
> > 
>
> 接口在实际中更多的作用是**制定标准**的。
> **<font color=green>接口的存在也是为了弥补类无法多继承的缺点。</font>**

<font color=red></font>
<font color=yellow></font>
<font color=green></font>
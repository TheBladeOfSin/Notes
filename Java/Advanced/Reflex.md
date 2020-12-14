## 反射

### 概述  

> （Java底层技术）在原有的OOP思想基础上从面到点的一个过程，通过字符串数据对类的成员控制的一种行为。
>
> <font color=red>关键字：Class</font> 
> <font color=green>Class类主要用于存储Java中所有类的描述信息，同时也是反射机制中不可或缺的一个主要部分，所有的反射操作都是从该类开始。并且Class类是唯一一个在Java中不是对象的类。</font>  

### 划分点

* 类加载方式
* 属性对象操作
* 方法对象操作

> * ####  类加载方式
>
> > 1. 对象名.getClass();
> >
> >    ``` java
> >    //先获取对应类的对象
> >    String str=new String();
> >    //利用反射通过对象获取类描述
> >    Class c1=str.getClass();
> >    
> >    //常用方法
> >    System.out.println("当前类名称："+c1.getName());	//获取类名称
> >    //获取类访问修饰符	--getModifiers()方法只能获取访问修饰符常量值
> >    //Modifier.toString(int)将访问修饰符常量值转换成字符串数据
> >    System.out.println("当前类访问修饰符："+Modifier.toString(c1.getModifiers());
> >    //通过类描述获取对象
> >    String s=(String)c1.newInstance();
> >    ```
> >
> >    
> >
> > 2. 类名.class;
> >
> >    ``` java
> >    //通过类名获取对应类对象
> >    Class c2=String.class
> >    ```
> >
> >    
> >
> > 3. Class.forName(类路径字符串);
> >
> >    ``` java
> >    //通过类路径获取对象
> >    Class c3=Class.forName("java.lang.String");
> >    ```
> >
> >    **类描述的核心结构**
> >
> >    * 属性
> >    
> >    * 方法
> >    
> >    * 构造方法
> >    
> ---
>
> * #### 属性对象操作
>
> > <font color=yellow>API：Field</font>
> > <font color=green>作用：通过类描述操作指定类中的属性，为该类的对象提供属性数据的获取和设置操作。</font> 
> >
> > ##### 实例：
> >
> > 指定类：Person
> >
> > ``` java
> > public class Person{
> >    	public String name;
> >    	private String secret="秘密";
> > }
> > ```
> >
> > 测试类：Test
> >
> > ``` java
> > //获取指定类描述
> > Class c=Class.forName("Person");
> > //获取属性对象
> > Field f1=c.getField("name");	//局限性：仅能获取类（及其父类）public属性成员
> > Field f2=c.getDeclaredField("name");// 能获取类本身的属性成员（包括私有、共有、保护）
> > 
> > /*
> >  * 常用方法
> >  */
> > System.out.println("属性对象名称："+f2.getName());	//获取属性名称
> > System.out.println("属性访问修饰符："+Modifier.toString(f2.getModifiers()));//获取属性访问修饰符
> > //getType()方法
> > System.out.println("属性对象类型："+f2.getType().getSimpleName());	//获取属性类型
> > 
> > //实例化Person对象
> > Person p=(Person)c.newInstance();
> > //设置属性值
> > f2.set(p,"name值");
> > //获取属性值
> > Field f3=c.getDeclaredField("secret");
> > //获取私有化属性数据
> > Object obj=f3.get(p);
> > System.out.println("获取的私有属性值："+obj);
> > 
> > //获取所有属性对象
> > Field[] fields=c.getDeclaredFields();
> > for(Field field:fields){
> >     //打开忽略访问修饰符的检查开关
> >     field.setAccessible(true);
> >     System.out.println(Modifier.toString(field.getModifiers()+" "+field.getType().getSimpleName+" "+field.getName()+"="+field.get(p));
> > }
> > ```
> >
>
> ---
>
>  * #### 方法对象操作
>
> > <font color=yellow>API：Method</font> 
> >
> > 通过类描述操作指定类中方法，在方法操作中需要烤炉两方面问题：
> > 1. 参数列表
> >    2. 返回值
> >
> >
> > 指定类：Demo
> >
> > ``` java
> > public class Demo{
> >     public void run1(){	//无参数无返回
> >         System.out.println("run1");
> >     }
> >     public String run2(int a,double b){	//有参数有返回
> >         return "run2";
> >     }
> > }
> > ```
> >
> > 测试类：Test
> >
> > ``` java
> > Class c=Class.forName("Demo");
> > //getDeclaredMethod("方法名",new Class[]{参数列表});
> > Method m1=c.getDeclaredMethod("run1", null);	//获取无参数无返回方法
> > System.out.println("方法名"+m1.getName());
> > System.out.println("访问修饰符"+Modifier.toString(m1.getModifiers()));
> > 
> > Method m2=c.getDeclaredMethod("run2", new Class[] {int.class,String.class});//获取有参数有返回方法
> > System.out.println("方法名"+m2.getName());
> > System.out.println("访问修饰符"+Modifier.toString(m2.getModifiers()));
> > System.out.println("返回类型"+m2.getReturnType());
> > 
> > //方法调用
> > m1.invoke(c,new Object[]{1,"2"});
> > ```
> >
> > 
> >
> > **构造方法： ** 
> >
> > <font color=yellow>API：Constructor</font> 
> >
> > - newInstance()通过指定的类描述创建该类对象，**可以根据传入的参数，调用任意构造函数**。
> > - Class.newInstance() 要求被调用的构造函数是可见的，即必须是public的; 
> > - **Constructor.newInstance() 在特定的情况下，可以调用私有的构造函数，<font color=red>需要通过setAccessible（true）实现</font>**。
> >
> > ``` java
> > //获取类描述
> > Class c=Class.forName("java.lang.String");
> > /*
> >  * Constructor没有invoke方法，只有newInstance方法
> >  */
> > 
> > //获取构造方法
> > Constructor ct1=c.getDeclaredConstructor(null);
> > System.out.println(ct1.getName());
> > //获取参数个数
> > System.out.println(ct1.getParameterCount());
> > //获取参数列表
> > 
> > //创建对象
> > String s=(String)ct2.newInstance(new Class[]{String.class});
> > //获取有参数构造方法调用
> > Constructor ct2.newInstance("String");
> > ```
> >
> > 
>
> ---



<font color=red></font>
<font color=yellow></font>
<font color=green></font>
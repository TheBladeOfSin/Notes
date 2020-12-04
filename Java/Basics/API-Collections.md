



## 集合框架

### 概述  

> util包中最重要的API组合，也是java中<font color=yellow>最大的一种数据存储容器</font>。

### 体系结构：

* Collection接口	父接口--> Itreable
> 子接口：
> 1. List接口
> > 实现类：ArrayList、LinkedList、Vector
> > 
>
> 2. Set接口
> > 实现类：HashSet、TreeSet
>
> * Map接口
> 实现类：HashMap
> ---
>
> #### List集合：
> > 实现原理：采用<font color=red>动态数组</font>的形式进行数据存储，存放在该集合中的数据是一种有序、可重复的数据。
> >
> > 实现类：
> > 1. **ArrayList**
> >
> >    ArrayList在集合操作中适合<font color=green>查询和修改</font>操作<font color=yellow>（默认初始化大小位10）</font>
> >
> >    ``` java
> >    //ArrayList的声明
> >    ArrayList list=new ArrayList();
> >    //常用方法
> >    list.add("data1");	//添加数据，依次存入数据
> >    list.add("data2");
> >    list.add(2,"data3");
> >    list.get(0);		//获取数据，通过索引
> >    ```
> >
> >    
> >
> > 2. **LinkedList**
> >
> >    LinkedList属于双向链表结构集合，每个元素都是以<font color=yellow>Node（节点）对象</font>进行存储，Node中包括三个内容，一是数据、二是上个节点的对象、三是下个节点的对象。适合于集合中进行<font color=green>添加和删除</font>操作。
> >
> > 3. **Vector**
> >
> >    Vector和 ArrayList 很相似，不同的是适用于线程操作中，可以解决线程<font color=green>同步问题</font>。<font color=red>**Vector中的操作是线程安全的**</font>。
> >
> ---
> #### Set集合：
> > 
> > Set集合是不允许出现重复元素，并且无序的集合，同时在数据存入到集合中时使用迭代器进行数据的迭代。
> >
> > * **HashSet**
> >
> >   
> #### Map集合：
> >
>
> #### Itreable
> >
> >

<font color=red></font>
<font color=yellow></font>
<font color=green></font>





集合框架		

 	5、Set集合
 			采用散列的方式进行数据存储，特征在于数据是无序的、不可重复，
 			同时在数据存入到集合中时使用迭代器进行数据的迭代。

   	6、Map集合
 			集成了Collection集合的特征，将数据以散列形式进行存储，同时
 			也实现了数据的定位获取，在存储数据的时候需要提供两组数据
 			内容为一个数据进行标识，该两组数据会由一个对象提供(Entry)，
 			Entry中数据标识以Key形式存在，值以value形式存在，数据结构
 			方法就是一个键值对的方式。
 			key必须是唯一的，而value可以重复的
 		
 		  实现类：
 		  		HashMap
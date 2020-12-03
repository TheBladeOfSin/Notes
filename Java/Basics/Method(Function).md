## Method(Function)

### 概述  

> 方法是语句的集合，它们在一起执行一个功能。
>
> - 方法是解决一类问题的步骤的有序组合。
>
> - 方法包含于类或对象中。
>
> - 方法在程序中被创建，在其他地方被引用。
>
> <font color=green> **[作用]：**</font>利于程序维护，提高程序开发效率，提高代码重用性，使程序简短清晰。

### 划分点

* 命名规则
* 方法分类
* 方法重载与重写

> * ####  命名规则
>
> > 定义方法包含的语法：
> >
> > 修饰符 返回值类型 方法名(参数类型 参数名1,参数类型 参数名2...) {
> >　　方法体语句;
> > 　　return 返回值;
> >}
> > 
> >示例：
> > 
> >``` java
> > public boolean isTrue(boolean flag){
> >    	/*方法体*/
> >         return flag;	//返回值
> > }
> > ```
>
> ---
>
> * #### 方法分类
>
> > * 构造方法（构造函数）
> >
> >   
> >
> > * **无参无返回：**
> > 修饰词 void 方法名() {
> > 　　方法体语句;
> > 　　return 返回值;
> > }
> > ``` java
> > public void methodName(){
> >     /* 方法体 */
> > }
> > ```
> >
> > * **无参有返回：**
> > 修饰词 返回类型 方法名() {
> > 　　方法体语句;
> > 　　return 返回值;
> > }
> > ``` java
> > public String methodName(){
> >     /* 方法体 */
> >     return "";
> > }
> > ```
> > * **有参无返回：**
> > 修饰词 void 方法名(参数类型 参数名1,参数类型 参数名2...) {
> > 　　方法体语句;
> > }
> > ``` java
> > public void methodName(int id,String name){
> >     /* 方法体 */
> > }
> > ```
> > * **有参有返回：**
> > 修饰词 返回类型 方法名(参数类型 参数名1,参数类型 参数名2...) {
> > 　　方法体语句;
> > 　　return 返回值;
> > }
> > ``` java
> > public String methodName(int id,String name){
> >     /* 方法体 */
> >     return "";
> > }
> > ```



<font color=red></font>
<font color=yellow></font>
<font color=green></font>
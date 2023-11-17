# **Java 从入门到入土**



## 	1.关于字符串

### 		1.1创建字符串的两种常用方式

​			

```java
 String a ="abc";
 String b = new String("abc");
 String c = new String("abc");
 System.out.println(b == c);//false
 System.out.println(a == b);//false
```

​     a创建的字符串将放在字符串常量池中（*串池*）并永久保留，当需要用时就会从串池中提取；b、c由于是**new**出来的，所以将会放在堆当中，b、c实际储存的是它的地址值。

### 		1.2字符串的比较***equals***

​     由于双等号比较的是两者地址值，所以显然 b != c, a != b（*a，b虽然都是储存到堆当中且记录内容相同，但由于地址值不同，判断结果就为false*）。

​    若想判断字符串的内容是否相等而非地址值，可以用Java提供的**equals**方法。

```java
 boolean flag = a.equals(b);
 System.out.println(flag);//true
 flag = b.equals(c);
 System.out.println(flag);//true
```

​	注意：equals返回值类型为布尔型。

### 		1.3字符串的相关方法



#### 1.31获取字符串长度***length()***

```java
String str = "abcde";
int len = str.length();//字符数组获取长度直接.length
System.out.println(len);//5
```



#### 			1.32字符串截取***substring()***

```java
String str1 = "1234567890";
//方法1
String str2 = str1.substring(0,4);//从0索引开始，3索引结束，包头不包尾
//方法2
String str3 = str1.substring(7);//截取从7索引开始的所有元素
 System.out.println(str2);//1234
 System.out.println(str3);//890
```

​	可用于类似手机号屏蔽（*13392141205 -> 133****1205*)、身份证中截取生日等操作

#### 		1.33字符串替代***replace()***

*注意：与**replaceAll()**不同的是，该方法不可识别正则表达式*

```java
String[] arr= {"2b","gun","sb"};//定义一个敏感词库
String talk = "2b,给爷gun";
for (String s : arr) {//增强for循环
     talk = talk.replace(s, "***");//把在数据中检测到的敏感词替代为***
     }
     System.out.println(talk);//***，给爷***
```

​	用法 ：*整个字符串字符串 . **replace**(要修改的部分字符串， 修改后的部分字符串)。* 

​	可用于敏感词的屏蔽等。

#### 1.34获取某一字符***charAt()***

```java
String str = "abcde";
char c1 = str.charAt(0);//获取字符串0索引的字符
char c2 = str.charAt(3);//获取字符串3索引的字符
System.out.println(c1);//a
System.out.println(c2);//d
```

**提示：关于字符数字与整型的转换**

​	*若想将字符串中获取的某一字符数字按照int类型输出，可通过以下方式*

```java
 int num = c - '0';
/*或int num = c - 48;
因为字符0所对应的ASCII值就是16进制的48*/
```

#### 1.35将字符串转换为字符数组***toCharArray()***

```java
String str = "abcde";
char[] c = str.toCharArray();
for (int i = 0; i < c.length; i++) {
    System.out.print(c[i] + ", ");
    }
//输出结果：a, b, c, d, e
```

#### 1.36将字符串按大写输出***toUpperCase()***

```java
String s = "Let us study Java";
//将字符串改为大写输出
 System.out.print(s.toUpperCase());//LET US STUDY JAVA
//将字符串改为小写输出
 System.out.print(s.toLowerCase());//let us study java
```



### 	1.4字符串的管理容器

​	当对字符串进行修改的时候，需要使用 **StringBuffer** 和 **StringBuilder** 类。

   和 String 类不同的是，**StringBuffer** 和 **StringBuilder** 类的对象能够被多次的修改，并且不产生新的未使用对象。

**StringBuilder** 类 **StringBuffer** 之间的最大不同在于 **StringBuilder** 的方法不是线程安全的（不能同步访问）。

由于 **StringBuilder** 相较于 **StringBuffer** 有速度优势，所以多数情况下建议使用 **StringBuilder** 类。

#### 		1.41***StringBuilder()***

​	**StringBuilder**提供的常用方法：

1.**append()**（添加字符串，也可添加整型、浮点型，但无法添加字符）

```java
//使用以下方式将字符转化成字符串
char c = 'a';
//1.
String str1 = c + "";
//2.
String str2 = String.valueOf(c);
//可将整型、浮点型转换成字符串
```

2.**insert()**（在指定索引插入指定字符串）

3.**reverse()**（反转字符串内容）

4.**length()**（获取当前字符串长度）

5.**toString()**（将**StringBuilder**管理的内容变成字符串变量）

```java
 StringBuilder sb = new StringBuilder();//括号内可添加字符串或或添加整型（代表规定容器长度）或留空
 sb.append(a).append(bcd).reverse();//链式编程
 String str = sb.toString();
  System.out.println(str);//dcba
```

​	可用于字符串的拼接、反转等操作。

#### 1.42***StringJoiner()***

​	**StringJoiner**提供的常用方法与**StringBuilder**相似，但创建对象有所不同。

注意：**add()**只可添加字符串

```java
  StringJoiner sj=new StringJoiner(", ","[","]");
//括号内放入分隔符号，0索引前的符号，最后一个索引后的符号
//可以只填分隔符号，需要用""括起来
  sj.add("1").add("2").add("3").add("4");
//添加字符串用add()方法
  int len= sj.length();//获取容器长度
  System.out.println(len);//12(包括额外添加的符号长度)
  String str = sj.toString();
  System.out.println(str);//[1, 2, 3, 4]
```

​	

------



## 2.关于集合

### 2.1集合的特点

1. 长度可以发生改变
2. 只能存储对象
3. 可以存储多种类型对象

### 2.2集合的书写格式

​	由于集合只能储存对象，故先创建一个类名为***User***的标准**JavaBean**为例

```java
public class User {
    private String name;
    private String number;

    public User(String name, String number) {
        this.name = name;
        this.number = number;
    }
    public User() {
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public String getNumber() {
        return number;
    }
    public void setNumber(String number) {
        this.number = number;
    }
}
```

​	再创建一个测试类

```java
import java.util.ArrayList;//使用前需要导包

public class Test {
        ArrayList<User> list = new ArrayList<>();
}

```

​	<>是泛型，只可以填写类名，显然可以将引用数据类型填入。但对于基本数据类型，需要填写其对应的类名（包装类），如：

***int -> Integer		double -> Double		byte -> Byte***

***short -> Short		float -> Float			long -> Long***				

其中这些包装类都是**Number**的子类

​	另外还有

​	***char -> Character		boolean -> Boolean*** 则是**Object**的直接子类



### 2.3集合的相关方法



#### 2.31将数据储存到集合***add()***

​	延续刚刚的测试类

```java
//创建两个User对象
 User u1 = new User("张三","13394857830");
 User u2 = new User("李四","13364830194");
//将两个对象按序储存到集合当中
  list.add(u1);
  list.add(u2);
```

​	*此时集合**list**所对应的0索引储存的是**u1**的数据，1索引储存的是**u2**的数据。*

```java
 User u3 = new User("王五","13358940371");
 list.add(1,u3);
```

​	若在**add()**方法中分别输入一个整型和一个对象，如上，则表示在集合**list**的1索引储存**u3**的对象，会将原来1索引的对象进行覆盖。如果索引超出范围（在这里如果大于1），则该 add() 方法抛出***IndexOutOfBoundsException*** 异常。



#### 2.32获取指定索引的数据***get()***

​	延续刚刚的测试类

```java
//获取0索引对应对象，再获取该对象的姓名方法如下 
System.out.println(list.get(0).getName());//张三
```



#### 2.33删除指定索引的数据***remove()***

​	延续刚刚的测试类

```java
//删除1索引对应的对象
list.remove(1);
```

​	注意，在删除1索引的对象后，集合**list**中的1索引并不为空，而是原本下一索引的对象向上移动1个索引

```java
//重新获取1索引的数据
System.out.println(list.get(1).getName());//王五
```

#### 2.34删除所有元素***clear()***

```java
Arraylist<String> list = new Arraylist<>();
list.add("a");
list.add("b");
list.add("c");
list.add("d");
System.out.println(list.size());//4
list.clear();
System.out.println(list.size());//0
```



#### 2.35获取集合长度***size()***

```java
//在执行了删除索引的操作后，获取集合长度
int len = list.size();
 System.out.println(len);//2 现在集合只储存了两个对象的数据
```



------



## 3.关于类



### 3.1工具类



​	工具类中可定义多种方法，当需要调用时，可以通过类名 . 方法名进行调用，无需实例化。

```java
//创建一个工具类
public class Util {
    //私有化构造方法（不让外界创建他的对象）
	private ArrayUtil(){}
    //需要定义为静态的，方便调用
	public static void fun1() {
	}
    public static void fun2() {
    }
}
```

​	再另一个类当中，直接调用方法即可。

```java
public class Main {
    public static void main(String[] args) {
  		Util.fun1();
        Util.fun2();
    }
}
```

### 3.2抽象类

​		抽象类是一个具有抽象结构的父类，一个可以被他的子类通用的类模式。方法的具体实现放在子类中，抽象类的抽象方法只有声明，不能有定义。

```java
//定义一个图形的抽象类
abstract class Shape(){//用abstract修饰
    abstract float area();//方法声明，也需要用abstract修饰
}
//定义一个实现类继承抽象类
class Circle extends Shape(){
    float r;
    //创建实现类的构造方法
    Circle(float r){
        this.r = r;
    }
    //方法实现
    public float area(){
        return (float) (3.14 * r * r);
    }
}
```

​	在创建对象时，只能创建实现类的对象

```java
public static void main(String[] args){
    Circle cir = new Circle(3);
    System.out.println(cir.area());
}
```

​	*抽象类的子类可以仍然是抽象类，但如果抽象类的子类是实现类，必须要实现父类的所有抽象方法。*

### 3.3内部类

#### 3.31成员内部类

​	写在成员位置，属于外部类的成员。只要可以修饰成员变量的修饰符，都可以用来修饰成员内部类（***private、default、protect、public、static*** ）。

```java
public class Car{//外部类
	String carName;
	int carAge;
	class Engine{//内部类
		String engineName;
		int engineAge;
	}
}
```

​	*注意：1.内部类可以调用外部类的私有成员和私有方法，但外部类无法调用内部类的私有成员和私有方法*

​		  *2.如果内部类的构造方法被私有化，则外界不能直接创建成员内部类的对象，只能在外部内的里面创建内部类的对象*



内部类获取外部类的成员变量

```java
public class Outer{
	private int a = 30;
	class Inner{
		private int a = 20;
		public void show(){
            int a = 10;
             System.out.println(a);//10
             System.out.println(this.a);//20
			System.out.println(Outer.this.a);//30
        }
    }
}
```

创建成员内部类的对象：

```java
public class Test1 {
    Outer.Inner oi = new Outer().new Inner();
}
```



#### 3.32静态内部类

​	静态内部类是一种特殊的成员内部类，只能访问外部类中的静态变量和静态方法，如果想要访问非静态的需要创建对象。

```java
public class Outer{
    //静态内部类
    static class Inner{
        public void show1(){
             System.out.println("非静态的方法被调用了");
        }
        public static void show2(){
			System.out.println("静态的方法被调用了");
        }
    }
}
```

创建静态内部类对象的格式

```java
public class Test2 {
    Outer.Inner oi = new Outer().Inner();
    //调用非静态方法
    oi.show1();//输出结果：非静态的方法被调用了
    //调用静态方法，直接用类名点到底
    Outer.Inner.show2();//输出结果：静态的方法被调用了
}
```



#### 3.33局部内部类

​	将内部类定义在方法里面，类似于方法里面的局部变量（用来修饰局部变量的都可以修饰局部内部类）。在外界无法直接使用，需要在方法内部创建对象并使用。

```java
 public class Outer{
	public void show(){
        //局部内部类
        public class Inner{
            String name = "张三";
            public void method(){
                System.out.println("局部内部类的方法");
            }
        }
        //创建局部内部类的对象
        Inner i = new Inner();
        System.out.println(i.name);//张三
        i.method()//局部内部类的方法
    }
}
```



#### 3.34匿名内部类

​	匿名内部类本质上是隐藏了名字的内部类。包含三部分：继承/实现 方法重写 创建对象

​	使用场景：

​		当方法的参数是接口或类时，以接口为例，可以传递这个接口的实现类对象，如果实现类只使用一次，就可以用匿名内部类简化代码

​	*书写格式 **new** 类名或接口名(){*

​	*重写方法*

​	*};*

​	1）创建一个接口

```java
public interface Swim{
    public abstract void swim();
}
```

​	在测试类当中编写匿名内部类

```java
public class Test3{
    public static void main(String[] args){
        new Swim(){
          @Override
            public void swim(){
                System.out.println("重写了游泳的方法");
            }
        };
    }
}
```

2）创建一个类

```java
public abstract Animal{
    public abstract void eat();
}
```

​	*现在想创建一个**Animal**类的子类**Dog**，并重写**eat()**方法，并在**main**方法中调用此方法。若**Dog**类只要用一次，还要单独定义一个类过于麻烦，就可以用匿名内部类简化代码。*

​	在测试类当中编写匿名内部类

```java
public class Test4{
    public static void main(String[] args) {
        method(
                new Animal() {
                    @Override
                    public void eat() {
                        System.out.println("狗吃骨头");
                    }
                }
        );//把整个对象当作参数传递给下方的Animal a
    }
    public static void method(Animal a){//定义一个方法
        a.eat();
    }
}
```

​	*传入参数后，就有 **Animal a =** 子类对象，形成多态，在执行**eat()**方法时执行编译看左边，运行看右边。*

### 3.4包装类

包装类是基本数据类型(***byte**、**short**、**char**、**int**、**long**、**float**、**double**、**boolean***)对应的引用类型

现以***int***的包装类***Integer***为例进行讲解

**获取包装类的方式(JDK5以前)**

```java
//利用构造方法获取Integer的对象
Integer i1 = new Integer(1);//括号内可以写入整型或字符串类型
Integer i2 = new Integer("1");
//利用静态方法获取Integer的对象
Integer i3 = Integer.valueOf(123);
Integer i4 = Integer.valueOf("123");
Integer i5 = Integer.valueOf("123",8);//表示123是8进制下的
System.out.println(i5);//83（把123当作8进制，再转成10进制进行打印）
```

注意：在实际开发中，-128~127之间的数据使用频率比较高，为了节约内存，使用静态方法获取时，***java***已经提前把这个范围内的每一个数据都创建好了对象，如果用到的话不会创建新的，而是返回已经创建好的对象

**自动装箱 / 自动拆箱(JDK5后)**

自动装箱：基本数据类型自动变成对应包装类

自动拆箱：包装类自动变成其对应基本数据类型

```java
//自动装箱
Integer i1 = 10;
//在底层，会自动调用静态方法valueOf得到一个Integer对象
Integer i2 = new Integer(10);
//自动拆箱
int i = i2;
```

**包装类常用成员方法**

以***Integer***为例

```java
//把整数转成二进制、八进制、十六进制
String str1 = Integer.toBinaryString(100);//100的2进制
String str2 = Integer.toOctalString(100);//100的8进制
String str3 = Integer.toHexString(100);//100的16进制
//将字符串类型的整数转成int类型的整数
String str = "123";
int i = Integer.parseInt(str);
System.out.println(str + 1);//1231
System.out.println(i + 1);//124
```

注意：8种包装类中，除了***Character***都有对应的***parseXxx***的方法进行类型转换

```java
String str = "true";
Boolean b = Boolean.parseBoolean(str);
System.out.println(b);//true
```



------



## 4.关于常用***API***

### 4.1***Math***

**Math**继承于**Object**，是一个用于进行数学计算的工具类。该类被**final**修饰，不能被继承

#### 4.11获取绝对值***abs()***

```java
 System.out.println(Math.abs(10));//10
 System.out.println(Math.abs(-10));//10
```

#### 4.12向上取整***ceil()***

​	进一法：往数轴的正方向进一

```java
 System.out.println(Math.ceil(3.14));//4.0
 System.out.println(Math.ceil(-3.14));//-3.0
```

#### 4.13向下取整***floor()***

​	去尾法：向负无穷的方向获取距离最近的整数

```java
 System.out.println(Math.floor(3.14));//3.0
 System.out.println(Math.floor(-3.14));//-3.0
```

#### 4.14四舍五入***round()***

```java
 System.out.println(Math.round(3.14));//3.0
 System.out.println(Math.round(3.55));//4.0
 System.out.println(Math.round(-3.14));//-3.0
 System.out.println(Math.round(-3.55));//-4.0
```

可以借助***round()***来实现浮点数保留几位小数

```java
//把一个有很多小数的数字赋值给a
double a = 1.23244354323;
//定义b为a保留两位小数的结果
double b = Math.round(a * 100) / 100.0;
System.out.println(a);//1.23244354323
System.out.println(b);//1.23
```



#### 4.15获取较大值***max()***

```java
 System.out.println(Math.max(20,30));//30
```

#### 4.16获取较小值***min()***

```java
 System.out.println(Math.min(20,30));//20
```

#### 4.17获取a的b次幂***pow()***

```java
System.out.println(Math.pow(2,3));//8
```

​	*I.如果第二个参数在 0~1 之间*

```java
System.out.println(Math.pow(4,0.5));//2.0（相当于4开根）
```

​	*II.如果第二个参数小于0*

```java
System.out.println(Math.pow(2,-2));//0.25
```



#### 4.18开算数平方根***sqrt()***

```java
System.out.println(Math.sqrt(4));//2
```

#### 4.19开立方根***cbrt()***

```java
System.out.println(Math.cbrt(8));//2
```



### 4.2***Arrays***

***Arrays*** 类是一个工具类，其中包含了数组操作的很多方法。这个 ***Arrays*** 类里均为 ***static*** 修饰的方法（***static*** 修饰的方法可以直接通过类名调用），可以直接通过 ***Arrays.xxx(xxx)*** 的形式调用方法。

#### 4.21将数组变成字符串***toString()***

```java
int[] arr = {1,2,3,4,5,6,7,8,9,10};
String str = Arrays.toString(arr);
System.out.println(str);//[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```



#### 4.22按照二分法查找元素***binarySearch()***

```java
int[] arr = {1,2,3,4,5,6,7,8,9,10};
//第一个参数传入整个数组，第二个参数传入要查找的元素，结果返回该元素的索引
System.out.println(Arrays.binarySearch(arr,10));//9
System.out.println(Arrays.binarySearch(arr,2));//1
System.out.println(Arrays.binarySearch(arr,20));//-11
```

注意：1.使用二分法前需要保证数组元素按序排列

​		  2.当要查找的元素不存在时，方法会返回 - 插入点 - 1 的值（例：在上述arr元素中查找20，由20大于数组最大值，插入点在索引			10，-10 - 1 = -11，返回值就是-11）

#### 4.23拷贝数组***copyOf()***

```java
int[] arr = {1,2,3,4,5,6,7,8,9,10};
//第一个参数传入老数组，第二个参数传入新数组长度
int[] newArr1 = Arrays.copyOf(arr,10);
System.out.println(Arrays.toString(newArr));//[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
int[] newArr2 = Arrays.copyOf(arr,2);
System.out.println(Arrays.toString(newArr2));//[1, 2]
```

注意：1.当新数组长度小于老数组长度时，会部分拷贝

​			2.当新数组长度等于老数组长度时，会完全拷贝

​			3.当新数组长度大于老数组长度时，会补上默认初始值

​			4.在方法的底层，调用的是System.arraycopy()方法

#### 4.24拷贝数组（指定范围）***copyOfRange()***

```java
int[] arr = {1,2,3,4,5,6,7,8,9,10};
//第一个参数传入老数组,第二个参数传入老数组的起始拷贝索引，第三个参数传入老数组的结束拷贝索引
int[] newArr = Arrays.copyOf(arr,0,9);
System.out.println(Arrays.toString(newArr));//[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

注意：该方法传入的索引值包头不包尾，包左不包右

#### 4.25填充数组***fill()***

```java
int[] arr = {1,2,3,4,5,6,7,8,9,10};
//第一个参数传入要填充的数组，第二个参数填入要填充的数字
Arrays.fill(arr,100);
System.out.println(Arrays.toString(arr));//[100, 100, 100, 100, 100, 100, 100, 100, 100, 100]
```

#### 4.26数组排序***sort()***

默认情况下，给基本数据类型按照升序排序

```java
//定义一个无序的整型数组 
int[] arr = {1,23,324,34,76,87,43,123,98};
//将元素由小到大排序
Arrays.sort(arr);
for (int i = 0; i < arr.length; i++) {
System.out.println(arr[i]);
}//23 34 43 76 87 98 123 324
```



若想按照降序排序，需要重载***sort()***方法：
*public static void sort(数组，排序规则)*

注意：该方法只能给引用数据类型的数据进行排序，如果数组是基本数据类型，需要转成其对应的包装类。

```java
Integer arr = {2,3,1,5,6,7,8,4,9};
/*第二个参数是一个接口，且接口的泛型与数组的数据类型保持一致
所以在调用方法时需要传递这个接口的实现类对象，作为排序的规则
但是这个实现类值只需要用一次，没必要单独写一个类，可以采取匿名内部类的方式*/

/*方法的底层原理：
利用插入排序 + 二分查找的方式进行排序。默认0索引的数据是有序序列，1索引~最后默认无序序列。遍历无序序列得到里面每一个元素，假设当前遍历得到的元素是A元素。把A往有序序列中进行插入。在插入的时候，利用二分查找确定A的插入点。用A和插入点进行比较，比较的规则就是compare方法的方法体。如果方法返回的是负数，用A继续和前面的数据进行比较。如果是正数，用A继续和后面的数据进行比较。如果返回的是0，也用A和后面的数据进行比较，直到能确定A的最终位置为止*/

/*compare方法的形参：
参数一(o1)：表示在无序序列中，遍历得到的每一个元素
参数二(o2)：表示有序序列中的元素*/

/*返回值为负数，表示当前要插入的元素是小的，放在前面；返回值是正数，表示当前要插入的元素是大的，放在后面；0：表示当前要插入的元素和现在的元素比是一样的，也放在后面*/

Arrays.sort(arr, new Comparator<Integer>(){
	@Override
	public int compare(Integer o1, Integer o2){
	return o2 - o1;
	}
});
```

*简单理解： o1 - o2 : 升序排列*

​					*o2 - o1 : 降序排列*



#### 4.27顺序流获取特定值***stream()***

```java
//获取数组最大值
System.out.println("最大值为"+Arrays.stream(arr).max().getAsInt());
//获取数组最小值
System.out.println("最小值为"+Arrays.stream(arr).min().getAsInt());
//获取数组平均值
System.out.println("平均值为"+Arrays.stream(arr).average().getAsDouble());
//获取数组总和
System.out.println("元素和为"+Arrays.stream(arr).sum());
```



### 4.3***System***

提供与系统相关的方法



#### 4.31终止当前运行的Java虚拟机***exit()***

```java
//方法的形参：状态码
//0：表示当前虚拟机是正常停止
//1：表示当前虚拟机是异常停止
System.exit(0);
```

#### 4.32返回当前系统的时间毫秒值形式***currentTimeMillis()***

```java
long l = System.currentTimeMillis();
System.out.println(l);
```

​	输出结果表示从时间原点（1970年1月1日8:00）到运行代码的时间点经历的毫秒值

#### 4.33数据拷贝***arraycopy()***

```java
int[] arr1 = {1,2,3,4,5,6,7,8,9,10};
int[] arr2 = new int[10];
/*把arr1中的数据拷贝到arr2中
参数一：数据源(要拷贝的数据从哪个数组来)
参数二：从数据源数组中的第几个索引开始拷贝
参数三：目的数组(要把数据拷贝到哪个数组中)
参数四：目的数组的索引
参数五：拷贝个数*/
System.arraycopy(arr1,0,arr2,4,3);
//遍历数组
for(int i = 0; i< arr2.length; i++){
    System.out.print(arr2[i] + " ");
}//0 0 0 0 1 2 3 0 0 0
```

​	*注意：*

​	*1.如果数据源数组和目的数字都是基本数据类型，那么两者类型必须一致，否则会报错*

​	*2.在拷贝的时候需要考虑数组的长度，如果超出范围也会报错*

​	*3.如果数据源数组和目的数字都是引用数据类型，那么子类类型可以赋值给父类类型*

```java
//已知Student类继承Person类，在Student有两个成员变量，分别是name和age，并有getName()和getAge()方法
Student s1 = new Student("张三",23);
Student s2 = new Student("李四",24);
Student s3 = new Student("王五",25);
Student[] arr1 = {s1,s2,s3};
Person[] arr2 = new Person[3];
//把arr1中对象的地址赋值给arr2
System.arraycopy(arr1,0,arr2,0,3);
//遍历数组arr2
for(int i = 0; i < arr2.length; i++){
    Student stu = (Student)arr2[i];//向下类型转换
     System.out.print(stu.getName() + ", " + stu.getAge());//张三， 23 李四， 24 王五， 25
}
```



### 4.4***Runtime***

#### 4.41获取当前系统的运行环境***getRuntime()***

```java
//获取Runtime的对象
Runtime r1 = Runtime.getRuntime();
System.out.println(r1);//java.lang.Runtime@7ef20235
```

#### 4.42停止虚拟机***exit()***

```java
Runtime.getRuntime.exit(0);
//虚拟机停止，不执行语句下方的代码
```

#### 4.43获得CPU线程数***availableProcessors()***

```java
 System.out.println(Runtime.getRuntime().availableProcessors());
```

#### 4.44JVM能从系统中获取总内存大小***maxMemory()***

```java
System.out.println(Runtime.getRuntime().maxMemory());//获取的是字节
System.out.println(Runtime.getRuntime().maxMemory() / 1024 / 1024);//获取的是兆
```

#### 4.45JVM已经从系统中获取总内存大小***totalMemory()***

```java
System.out.println(Runtime.getRuntime().toalMemory());
```

​	*注意：单位是byte*

#### 4.46JVM剩余内存大小***freeMemory()***

```java
 System.out.println(Runtime.getRuntime().freeMemory());
```

#### 4.47运行**cmd**命令***exec()***

```java
 System.out.println(Runtime.getRuntime().exec("写入命令"));
```

### 4.5***Object***

​	**Object**是**Java**中的顶级父类。所有的类都直接或间接继承于**Object**类。

**Object**的构造方法

```java
public Object() //只有空参构造
```

**Object**的成员方法

#### 4.51返回对象的字符串表现形式***toString()***

```java
Object obj = new Object();
String str = obj.toString();
 System.out.println(str);//java.lang.Object@a119d7047
```

​	*其中@是固定格式，@前面是包名+类名，后面是对象的地址值。*

​	如果直接将对象名进行输出

```java
System.out.println(obj));//java.lang.Object@a119d7047
```

​	输出的结果与上方一致

​	*因为输出语句是由**System**(类名) +**out**(**System**里的静态变量) [**System.out**获取打印的对象]+**println**()(方法) 组成。如果打印的是一个对象，底层会调用对象的**toString**方法，把对象变成字符串，然后打印在控制台上，最后进行换行处理。*

由于在实际开发当中，返回地址值并没有什么作用，所以一般可以选择重写父类的**toString()**方法以达到反正我们需要的内容的目的。

```java
//已知定义了一个类，类当中有姓名和年龄两个成员变量，现在重写toString()来返回这两个变量值
@Override
public String toString(){
    return name + ", " + age;
}
```



#### 4.52比较两个对象是否相等***equals()***

先写一个具有标准***JavaBean***的***Student***类，里面具有***name***和***age***两个成员变量。

再写一个测试类，创建两个***Student***对象，并用***equals***比较两个对象

```java
Student s1 = new Student("张三",23);
Student s2 = new Student("张三",23);
boolean result = s1.equals(s2);
System.out.println(result);//false
```

​	*默认情况下，**equals**会比较两个对象的地址值是否相等。*

​	*若想比较两个对象属性值是否相等，需要在类中重写**equals()**方法*

```java
@Override
public boolean equals(Object o){
if(this == o) return true;//如果两个对象地址值相同，对象内容一定也相同
Student stu = (Student) o;//把Object对象o向下转型
return age == stu.age && Objects.equals(name,stu.name);//只有当两个对象所有属性相等时，才返回true
}
```

​	如果比较两个没有继承关系的对象，如下

```java
String s = "abc";
StringBuilder sb = new StringBuilder("abc");
System.out.println(s.equals(sb));//false
System.out.println(sb.equals(s));//false
```

​	*由于第一个**equals()**是被字符串**s**调用，而在**String**类中重写了**equals()**方法（如果传入的两个参数都是字符串，则比较两个字符串的内容，否则直接返回**false**）*

​	*第二个**equal()**是被**StringBuilder**对象调用，而在**StringBuilder**中并没有重写该方法，只是调用了**Object**的**equals()**，比较的仍是两个对象的地址值，显然s和sb记录的地址值是不同的，所以返回**false**。*



#### 4.53对象克隆***clone()***

​	把A对象的属性值完全拷贝给B对象，也叫对象拷贝，对象复制

1.浅克隆（浅拷贝）：拷贝后的对象和原对象共用一个地址值，其中一个对象发生变化另一个也会随之变化

​	先创建一个类

```java
public class User{
int id;
String username;
String password;
int[] data = {...}
    //具有空参和全参构造方法
    //具有完成get和set方法
    //重写了toString方法
}
```

​	在测试类中创建对象

```java
int[] data = {1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,0};
User u1 = new User(1,"zhangsan","1234qwer",data);
```

由于***clone()***方法的修饰符是***protected***，只能被本包或其他包中的子类使用，且***Object***是定义在***java.lang***包下，无法将代码写在***lang***包。当需要使用***clone()***方法时，只能重写方法。

​	在**User**类当中重写**clone**方法

```java
@Override
protected Object clone() throws CloneNotSupportedException{
	//调用父类中的clone()方法,相当于让java帮我们克隆一个对象，并把克隆之后的对象返回
	return super.clone();
}
```

回到测试类中

```java
//克隆对象
//由于代码帮我们克隆出来的是一个用户对象，还需要做一个强转
User u2 = (User)u1.clone();
System.out.println(u1);//角色编号：1，用户名：zhangsan1，密码：1234qwer,游戏进度：[1,2,3,4,5,6,7,...]
System.out.println(u2);//角色编号：1，用户名：zhangsan1，密码：1234qwer,游戏进度：[1,2,3,4,5,6,7,...]

```

*书写步骤： 1.重写**Object**中的**clone()**方法*

​					*2.让**javabean**类中实现**Cloneable**接口（标记接口）*

​					*3.创建原对象并调用**clone()***



2.深克隆（深拷贝）：两个对象相互独立，互不影响

​	具体而言，深克隆会将基本数据类型拷贝过来，字符串会复用，引用数据类型会重新创建新的

​	重写***User***类中的***clone()***方法

```java
@Override
protected Object clone() throws CloneNotSupportedException{
	//先把被克隆的对象中的数据获取出来
    int[] data = this.date;
    //创建新的数组
    int[] newData = new int[data.length];
    //拷贝数组中的数据
    for(int i = 0; i < data.length; i++){
        newData[i] = data[i]
	}
    //调用父类中的方法克隆对象
    User u =(User)super.clone();
    //因为父类中的克隆发给发是浅克隆，替换克隆出来对象中的数组地址值
    u.data = newData;
    return u;
}
```

回到测试类当中

```java
//u1不变，将u1的属性值克隆给u2
//改变u1中的数组
int[] arr = u1.getData();
arr[0] = 100;
System.out.println(u1);//角色编号：1，用户名：zhangsan1，密码：1234qwer,游戏进度：[100,2,3,4,5,6,7,...]
System.out.println(u2);//角色编号：1，用户名：zhangsan1，密码：1234qwer,游戏进度：[1,2,3,4,5,6,7,...]
```



### 4.6***Objects***

***Objects***是一个工具类，提供了一些方法去完成一些功能。

#### 4.61***equals()***

​	先做非空判断，比较两个对象（值为***null***的对象无法调用方法，程序会报错）

​	先创建一个Student类

```java
public class Student{
String name;
int age;
//已定义好构造方法
//重写equals()方法（使其比较对象内部的属性值）
@Override
    public boolean equals(Object o){
        if(this == 0) return true;
        if(o == null || getClass() != o.getClass()) return false;
        Student student = (Student)o;
        return age == student.age && Objects.equals(name,student.name);
    }
    
}
```

​	在测试类当中

```java
Student s1 = null;
Student s2 = {"zhangsan",23};
//比较两个对象的属性值是否相同
boolean result = Objects.equals(s1,s2);
System.out.println(result);//false
```

​	*方法的底层会判断**s1**是否为**null**，如果为**null**，直接返回**false**。如果**s1**不为**null**，那么就利用**s1**再次调用equals()方法。此时**s1**是**Student**类型，所以最终会调用**Student**中的**equals()**方法。如果没有重写，比较地址值，如果重写了，就比较属性值*

#### 4.62***isNull()***以及***nonNull()***

***isNull()***判断对象是否为***null***，为***null***返回***ture***，否则 返回***false***

***nonNull()***反之

```java
Student s3 = new Student();
System.out.println(Objects.isNull(s3));//false
Student s4 = null;
System.out.println(Objects.isNull(s4));//true

System.out.println(Objects.nonNull(s3));//true
System.out.println(Objects.nonNull(s4));//false
```



### 4.7**BigInteger**

#### 4.71几种构造方法

​	**获取随机大整数**

​	*public BigInteger(int num,Random rnd) 获取最大整数，范围[0 ~ 2 的num次方-1]*

```java
Random r = new Random;
BigInteger bd1 = new BigInteger(4,r);//范围： 0 ~ 15
System.out.println(bd1);//生成 0-15的随机数
```

​	**获取指定大整数**

​	*public BigInteger(String val)* 

​	字符串中必须是整数，否则会报错

```java
BigInteger bd2 = new BigInteger("100");
System.out.println(bd2);//100
BigInteger bd3 = new BigInteger("9999999999999999999999999999999999999999999999999999999999990");
System.out.println(bd3);//9999999999999999999999999999999999999999999999999999999999990
```

​	**获取指定进制大整数**

​	*public BigInteger(String val，int radix)* 

```java
BigInteger bd4 = new BigInteger("100",10);//表示10进制的100
System.out.println(bd4);//100
BigInteger bd5 = new BigInteger("100",2);//表示2进制的100
System.out.println(bd5);//4
```

​	**静态方法获取*BigInteger*的对象**

​	该方法能表示的范围比较小，在long的取值范围之内，无法接收超过long的范围的整数

```java
BigInteger bd6 = BigInteger.valueOf(100);
System.out.println(bd6);//100
```

​	该方法在内部对常用的数字（-16 ~ 16）进行了优化：提前把-16 ~16 先创建好BigInteger的对象，如果多次出现不会重新创建新的。

```java
BigInteger bd7 = BigInteger.valueOf(16);
BigInteger bd8 = BigInteger.valueOf(16);
System.out.println(bd7 == bd8);//true
//没被优化的数字会重新创建对象
BigInteger bd9 = BigInteger.valueOf(17);
BigInteger bd10 = BigInteger.valueOf(17);
System.out.println(bd9 == bd10);//flse
```

​	对象一旦创建，BigInteger内部记录的值不能发生改变。只要进行计算都会产生一个新的BigInteger对象



#### 4.72常用成员方法

```java
//创建两个BigInteger对象
BigInteger bd1 = BigInteger.valueof(10);
BigInteger bd2 = BigInteger.valueof(5);
//加法add
BigInteger bd3 = bd1.add(bd2);
System.out.println(bd3);//15
//减法subtract
//乘法multiply
//除法（获取商）divide
//除法（获取商和余数）divideAndRemainder
BigInteger[] arr = bd1.divideAndRemainder(bd2);
System.out.println(arr.length);//2(0索引为商，1索引为余数)
System.out.println(arr[0]);//2
System.out.println(arr[1]);//0
//比较两数是否相同equals
//次幂pow
BigInteger bd4 = bd1.pow(2);//参数为int型
System.out.println(bd4);//100
//返回较大值/较小值max/min
//转换为int型整数intvalue
BigInteger bd6 = BigInteger.valueof(1000);
int i = bd6.intvalue();
//转换为long型整数longvalue
//转换为double型整数doublevalue
```



### 4.8***BigDecimal***

#### 4.81几种构造方法

​	**通过传递double类型的小数来创建对象**

​		*public BigDecimal(double val)*

​	*这种方式有可能是不精确的，不建议使用*

​	**通过传递字符串表示的小数来创建对象**

​	*public BigDecimal(String val)*

```java
BigDecimal bd1 = new BigDecimal("0.01");
BigDecimal bd2 = new BigDecimal("0.09");
System.out.println(bd1);//0.01
System.out.println(bd2);//0.09
```



​	**通过静态方法获取对象**

​	*public static BigDecimal valueOf(double val)*

​	如果要表示的数字不大，没有超出double的取值范围，建议使用静态方法

```java
BigDecimal bd3 = BigDecimal.valueOf(10);
```

​	如果传递的是[0,10]之间的整数，那么方法会返回已经创建好的对象，不会重新new



#### 4.82常用成员方法

```java
BigDecimal bd1 = BigDecimal.valueOf(10.0);
BigDecimal bd2 = BigDecimal.valueOf(2.0);
//加法add
BigDecimal bd3 = bd1.add(bd2);
System.out.println(bd3);//12.0
//减法subtract
//乘法multiply
//除法divide
//写法1（除得尽）
BigDecimal bd4 = bd1.divide(bd2);
System.out.println(bd4);//5
//写法2（除不尽）
BigDecimal bd5 = BigDecimal.valueOf(10.0);
BigDecimal bd6 = BigDecimal.valueOf(3.0);
BigDecimal bd7 = bd5.divide(bd6,2,RoundingMode.HALF_UP);//参数分别为被除数，保留小数位数，舍入模式
System.out.println(bd7);//3.33
```



### 4.9正则表达式



用来判断字符串是否符合规定的格式

#### 4.91基本规则

|        字符串类 | 只匹配一个字符                |
| --------------: | ----------------------------- |
|           [abc] | 只能是a,b或者c                |
|          [^abc] | 除了a,b,c之外的任何字符       |
|        [a-zA-Z] | a到z，A到Z                    |
|      [a-d[m-p]] | a到d，或m-p                   |
|    [a-z&&[def]] | d,e,f(交集)                   |
| `[a-z&&[^m-p]]` | a到z,除了m到p(等同于[a-lq-z]) |



| 预定义字符 | 只匹配一个字符                 |
| ---------: | ------------------------------ |
|          . | 任何字符                       |
|         \d | 一个数字:[0-9]                 |
|         \D | 非数字                         |
|         \s | 一个空白字符                   |
|         \S | 非空白字符                     |
|         \w | 英文、数字、下划线[a-zA-Z_0-9] |
|         \W | 一个非单词字符                 |



| 数量级 |                     |
| -----: | ------------------- |
|     X? | X，1次或0次         |
|     X* | X，0次或多次        |
|     X+ | X，1次或多次        |
|   X{n} | X，正好n次          |
|  X{n,} | X，至少n次          |
| X{n,m} | X，至少n但不超过m次 |



**其他书写格式**

检测字符串是否满足某几个字符组合时，可以用“|”表示并集：(字符组合1|字符组合2|字符组合3) “()"表示分组

检测字符串无视字母大小写时，可以用(?i)字母的格式书写：a(?i)b (即ab、aB均满足要求)



#### 4.92在字符串方法中的使用



**判断字符串是否满足正则表达式的规则**

​	*public boolean matches(String regex)*

```java
//判断是否与正则表达式匹配
System.out.println("a".matches("[abc]"));//true
```



**按照正则表达式的规则进行替换**

​	*public String replaceAll(String regex,String newStr)*

```java
//把下面字符串出现的字母和数字删除
String s = "这是ab3jcbs1j一段idfh6w5ifh文本";
//第一个参数写入正则表达式，第二个参数写入要替换的内容
//所有满足该正则表达式的内容都会被替换
String result = s.replaceAll("[\\w&&[^_]]+","");
System.out.println(result);//这是一段文本
```



**按照正则表达式的规则切割字符串**

​	*public String[] split(String regex)*

```java
String s = "这是ab3jcbs1j一段idfh6w5ifh文本";
String[] arr = s.split("[\\w&&[^_]]+");
for(int i = 0;i < arr.length;i++){
    System.out.println(arr[i]);
}//这是		一段		文本
```



#### 4.93捕获分组和非捕获分组

正则表达式当中以"()"进行分组，从1开始，连续不间断。以左括号为基准，最左边的是第一组，其次为第二组，以此类推

**捕获分组**

​	后续还要继续使用本组的数据。正则内部使用"\\\1"，正则外部使用"$”组号

```java
//需求1：判断一个字符串的开始字符和结束字符是否一致？只考虑一个字符
//"\\+组号"表示把第x组的内容再拿出来用一次
String regex1 = "(.).+\\1";
System.out.println("a123a".matches(regex1));//true
System.out.println("17891".matches(regex1));//true
System.out.println("&abc&".matches(regex1));//true
System.out.println("a123b".matches(regex1));//false
//需求2：判断一个字符串的开始字符和结束字符是否一致？可以有多个字符
String regex2 = "(.+).+\\1";
System.out.println("abc123abc".matches(regex2));//true
System.out.println("123789123".matches(regex2));//true
System.out.println("^&*abc^&*".matches(regex2));//true
System.out.println("abc123bcd".matches(regex2));//false
//需求3：判断一个字符串的开始字符和结束字符是否一致？开始部分内部每个字符也要一致
String regex3 = "((.)\\2*).+\\1";
System.out.println("aaa123aaa".matches(regex3));//true
System.out.println("111789111".matches(regex3));//true
System.out.println("**bc**".matches(regex3));//true
System.out.println("aaa123aab".matches(regex3));//false
```

案例分析

将字符串重复内容进行删除

```java
String str =  "这这这是是一一一一段段段文文本";
//$1表示把正则表达式中第一组的内容再拿出来用（在正则表达式之外用）
String result = str.replaceAll("(.)\\1+","$1");
System.out.println(result);//这是一段文本
```

**非捕获分组**

*分组之后不需要再用本组数据，仅仅是把数据括起来。其中，(?:)、(?=)、(?!)都是非捕获组分，是不占用组号的。一般情况下更多的使用(?:)，因为它既包含左括号前面的数据，也包含冒号后面的数据。*



### 4.10爬虫

**爬取本地信息**

```java
/*有如下文本，请按照要求爬取数据
Java自从95年问世以来，经历了很多版本，目前企业中用的最多的是Java8和Java11，因为这两个是长期支持的版本，下一个长期支持版本是Java17，相信在未来不久Java17也会逐渐登上历史舞台
要求：找出里面所有的JavaXX*/
String str = "Java自从95年问世以来，经历了很多版本，目前企业中用的最多的是Java8和Java11，因为这两个是长期支持的版本，下一个长期支持版本是Java17，相信在未来不久Java17也会逐渐登上历史舞台";
//1.获取正则表达式
Pattern p = Pattern.compile("Java\\d{0,2}");
//2.获取文本匹配器的对象
Matcher m = p.matcher(str);
//利用循环获取
while(m.find()){
    String s = m.group();
    System.out.println(s);
}//Java Java8 Java11 Java17 Java17 
```

**有条件的爬取数据**

*将上述文本按照不同要求爬取数据：*

*需求1：爬取版本号为8,11,17的Java文本，但是只要Java，不显示版本号。*

```JAva
//为了更好的区分，设置每个java的大小写数量不同
String str = "java自从95年问世以来，经历了很多版本，目前企业中用的最多的是Java8和JAva11，因为这两个是长期支持的版本，下一个长期支持版本是JAVa17，相信在未来不久JAVA17也会逐渐登上历史舞台";
//1.定义正则表达式
//第二个"?"表示前面的数据(Java忽略大小写)，"="表示在Java后面拼接什么，可以拼8、11或17，但实际获取的还是括号前的数据
String regex1 = "((?i)Java)(?=8|11|17)";
Pattern p = Pattern.compile(regex1);
Matcher m = p.matcher(s);
while(m.find()){
    String s = m.group();
    System.out.println(s);
}//Java JAva JAVa JAVA,没有第一个纯小写的java

```

*需求2：爬取版本号为8,11,17的Java文本，爬取结果保留版本号*

```java
//第二个"?"表示前面的数据，":"表示获取整体
String regex2 = "((?i)Java)(?:8|11|17)";
Pattern p = Pattern.compile(regex2);
Matcher m = p.matcher(s);
while(m.find()){
    String s = m.group();
    System.out.println(s);
}//Java8 JAva11 JAVa17 JAVA17

```

*需求3：爬取除了版本号为8,11,17的Java文本*

```java
//"！"表示去除
String regex3 = "((?i)Java)(?!8|11|17)";
Pattern p = Pattern.compile(regex3);
Matcher m = p.matcher(s);
while(m.find()){
    String s = m.group();
    System.out.println(s);
}//java

```



**贪婪爬取**

在爬取数据时尽可能多的获取数据

```java
String s = "abbbbbbbbbbb";
String regex1 = "ab+";
//贪婪爬取：abbbbbbbbbbb
//非贪婪：ab
```

*Java中默认的就是贪婪爬取*

```java
Pattern p = Pattern.complie(regex1);
Matcher m = p.matcher(s);
while(m.find()){
	System.out.println(m.group());
}//abbbbbbbbbbb
```

**非贪婪爬取**

在爬取数据时尽可能少的获取数据

​	*如果在数量词+ 后面加上？，那么就是非贪婪爬取*

```java
String regex2 = "ab+?";
Pattern p = Pattern.complie(regex2);
Matcher m = p.matcher(s);
while(m.find()){
	System.out.println(m.group());
}//ab
```



### 4.11日期类

#### 4.111***Date***

***Date**在***java.util.Date***包下

**两种构造方法**

```java
//创建对象表示一个时间使用空参构造
Date d1 = new Date();
System.out.println(d1);//Sat Jul 16 18:43:23 CST 2022
//创建对象表示一个指定时间
Date d2 = new Date(0L);//表示从时间原点开始过了0毫秒的时间
System.out.println(d2);//Thu Jan 01 08:00:00 CST 1970
```

**常用方法**

​	设置/修改毫秒值

```java
*public void setTime(long time)*
```

​	获取时间对象的毫秒值

```java
*public long getTime()*
```

**案例分析**

```java
//修改时间
d2.setTime(1000L);//表示从时间原点开始过了1000毫秒的时间
System.out.println(d2);//Thu Jan 01 08:00:01 CST 1970
//获取当前时间的毫秒值
long time = d2.getTime();
System.out.println(time);//1000
```

#### 4.112***SimpleDateFormat***

作用：1.格式化：把时间变成我们指定的格式

​			2.解析：把字符串表示的时间变成***Date***对象

**两种构造方法**

```java
//利用空参构造创建SimpleDateFormat对象
SimpleDateFormat sdf1 = new SimpleDateFormat();
Date d1 = new Date(0L);
//格式化
String str1 = sdf1.format(d1);
System.out.println(str1);//1970/1/1 上午8:00

//利用带参构造创建对象，指定格式
SimpleDateFormat sdf2 = new SimpleDateFormat("yyyy年MM月dd日 HH:mm:ss");
String str2 = sdf2.format(d1);
System.out.println(str2);//1970年01月01日 08:00:00

```

定义了以下模式字母：

| 字母 |    日期或时间元素    |  表示  |
| :--: | :------------------: | :----: |
|  y   |          年          |  Year  |
|  M   |      年中的月份      | Month  |
|  d   |     月份中的天数     | Number |
|  E   |     星期中的天数     |  Text  |
|  a   |      Am/pm标记       |  Text  |
|  H   | 一天中的小时数(0~23) | Number |
|  m   |    小时中的分钟数    | Number |
|  s   |     分钟中的秒数     | Number |
|  S   |        毫秒数        | Number |

**常用方法**

​	格式化(日期对象 -> 字符串)

```java
*public final String format(Date date)*
```

​	解析(字符串 -> 日期对象)

```java
*public Date parse(String source)*
```

**案例分析**

```java
//定义一个字符串表示时间
String str = "2023-11-11 11:11:11";
//利用空参构造创建SimpleDateFormat对象，创建对象的格式要和字符串的格式完全一致
SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
Date date = sdf.parse(str);
System.out.println(date);//Sat Nov 11 11:11:11 CST 2023
//创建Date对象后，可以把当前时间毫秒值获取出来
System.out.println(date.getTime());//1699672271000
//获取毫秒值后，可以对时间进行加减判断
```

#### 4.113***Calendar***

Calendar代表了系统当前时间的日历对象，可以单独修改、获取时间中的信息。其中Calendar是一个抽象类，不能直接创建对象

**获取Calendar对象的方法**

*public static Calandar getInstance()*

```java
Calendar c = Calendar.getInstance();//默认表示当前时间
```

*注意：1.日历对象是一个数组，会把时间中的纪元、年、月、日、分、秒、星期等信息放入一个数组中，0索引代表纪元，1：年，2：			月，5：日（一个月中的第几天）*

​			*2.月份的范围是0~11，0代表一月份，1代表二月份，以此类推*

​			*3.在星期1~7当中，1代表周日，2代表周一，以此类推，7代表周六*



**Calendar的常用方法**

**获取日期对象**

```java
*public final Date getTime()*
```

**给日历设置日期对象**

*public final setTime(Date date)*

```java
Date d = new Date(0L);
c.setTime(d);//此时的Calendar对象保存的是时间原点的对应时间信息
```

**获取时间毫秒值**

```java
*public long getTimeMillis()*
```

**给日历设置时间毫秒值**

```java
*public  viod setTimeMillis(long millis)*
```

**取日历中的某个字段信息**

*public int get(int field)*

```java
int year = c.get(1);
int month = c.get(2) + 1;//月份的范围是0~11
int date = c.get(3);
System.out.println(year + "年" + month + "月" + date + "日");//1970年1月1日
//为了提高阅读性，java在Calendar类中，把索引对应的数组都定义成常量
year = c.get(Calendar.YEAR);
month = c.get(Calendar.MONTH);
date = c.get(Calendar.DAY_OF_MONTH);
int week = c.get(Calendar.DAY_OF_WEEK);
System.out.println(year + "年" + month + "月" + date + "日 " + week);//1970年1月1日 5
```

为了让***Calendar***记录的星期信息符合中国人的阅读习惯，可以定义一个方法(查表法)

```java
//传入对应数字1~7，返回对应的星期
public static String getWeek(int index){
String[] arr = {"","星期日","星期一","星期二","星期三","星期四","星期五","星期六"}
return arr[index];
}
```

修改一下输出语句

```java
System.out.println(year + "年" + month + "月" + date + "日 " + getWeek(week));//1970年1月1日 星期四
```

**修改日历的某个字段信息**

*public void set(int filed,int value)*

```java
c.set(Calendar.YEAR,2000);
c.set(Calendar.MONTH,11);
System.out.println(year + "年" + month + "月" + date + "日 " + getWeek(week));//2000年12月1日 星期五
//如果修改的月份大于11,会把时间顺着往后排，会把年份也进行调整
c.set(Calendar.MONTH,12);
System.out.println(year + "年" + month + "月" + date + "日 " + getWeek(week));//2001年1月1日 星期一
```



**为某个字段增加/减少指定的值**

*public void add(int field,int amount)*

```java
//调用add方法在这个基础上增加一个月
c.add(Calendar.MONTH,1);//2023,2,1
//如果第二个参数是负数，则会向前减一个月
```



### 4.12***Lambda***表达式

​	***Lambda***表达式是***JDK8***开始后的一种新语法形式，可以用来简化匿名内部类的书写，但只能简化函数式接口（有且仅有一个抽象方法的接口，接口上方可以加***@Functionallnterface***注解）的匿名内部类的写法。

案例分析

```java
//以Arrays.sort()方法为例
Integer[] arr = {2,3,1,5,6,7,8,4,9};
//匿名内部类写法
Arrays.sort(arr, new Comparator<Integer>(){
	@Override
	public int compare(Integer o1, Integer o2){
	return o1 - o2;
	}
});
/*使用Lambda表达式，将方法名前的所有信息去除，在形参的括号后加上箭头->即可*/
Arrays.sort(arr,(Integer o1, Integer o2) -> {
    return o1 - o2;
	}
);
```

***Lambda**的省略写法*

*1.参数类型可以不写*

*2.如果只有一个参数，参数类型可以省略，同时()也可以省略*

*3.如果**Lambda**表达式的方法体只有一行，大括号、分号、**return**可以省略不写，需要同时省略*

```Java
//省略写法
Arrays.sort(arr,(o1, o2) -> o1 - o2);
```



------



## 5.关于异常

​	**Java**中的异常是指**Java**程序在运行时可能出现的错误或非正常情况。

### 5.1***Throwable***类及其常用方法



​	**Java**提供了大量的异常类，每一个异常类都表示一种预定义的异常，这些异常类都继承**java.lang**包下的**Throwable**类。

**Throwable的子类**

它有两个直接子类**Error**和**Exception**，其中**Error**代表程序中产生的错误，**Exception**表示程序中产生的异常。



**常用方法**

```java
String getMessage()*返回异常的消息字符串（异常信息）*

String toString()*返回异常的简单信息描述（异常类名 + 异常信息）* 

void printStackTrace()*获取异常类名和异常信息，以及异常出现在程序中的位置，把信息输出在控制台（与不处理时控制台给的报错信息一致）*
```



### 5.2运行异常与编译异常

**编译异常**

*编译异常必须进行处理，否则程序无法正常运行。在**Exception**类中，除了**RuntimeException**类及其子类，**Exception**的其他子类都是编译异常。**Java**编译器会对异常进行检查，如果出现异常就必须进行处理，否则程序无法通过编译。*

**运行异常**

*运行异常即使不编写异常代码处理，依然可以通过编译。*

*在Java中，常见的运行异常有*

|         方法声明          |    功能描述    |
| :-----------------------: | :------------: |
|    ArithmeticException    |    算术异常    |
| IndexOutOfBoundsException |  索引越界异常  |
|    ClassCastException     |  类型转换异常  |
|   NullPointerException    |   空指针异常   |
|   NumberFormatException   | 数字格式化异常 |

异常发生后，默认会在异常的代码那自动创建一个异常对象，异常会从方法中出现的点这里抛出给调用者，调用者最终抛出给**JVM**。**JVM**接收到异常对象后，先在控制台直接输出异常栈信息数据，然后直接从当前执行的异常点结束当前程序。



### 5.3异常处理及语法

在**Java**中，通过**try**、**catch**、**finally**、**throw**、**throws**这5个关键字进行异常对象的处理。

#### 5.31***try...catch***

为了使发生异常后的程序代码正常执行，程序需要捕获异常并进行处理。**try...catch**语句格式如下：

```java
try{
代码块
}catch(Exception Type e){
代码块
}
```

​	*注意：1.**try**代码块是必需的*

​	*2.**catch**代码块和**finally**代码块都是可选的，但**catch**代码块和**finally**代码块至少要出现一个*

​	*3.**catch**代码块可以有多个，但捕获父类异常的**catch**代码块必须位于捕获子类异常的**catch**代码块后面*

​	*4.**catch**代码块必须位于**try**代码块之后*

案例演示

```java
try{
int result = 3 / 0;
System.out.println(result);//这句不会执行
}catch(Exception e){//对异常进行处理
    System.out.println("捕获的异常信息为：" + e.getMessage());//会执行
}//异常已被处理
 System.out.println("程序继续向下执行");
/*控制台显示的运行结果为
捕获的异常信息为：/ by zero
程序继续向下执行*/
```

​	*注意：在**try**代码块中，发生异常语句后面的代码时不会被执行的*

#### 5.32***finally***

**finally**代码块可以使语句无论是否发生异常都要执行。如果程序发生异常但是没有被捕获到，在执行完**finally**代码中的代码之后，程序会中断执行。

**finally**语句格式如下：

```java
try{
代码块
}catch(Exception Type e){
代码块
}finally{
代码块
}
```

​	*注意：**finally**代码块必须位于所有**catch**代码块之后*

#### 5.33***throws***

**Java**运行在方法的后面使用**throws**关键字声明该方法有可能发生的异常。调用者在调用方法时，可以明确知道该方法有异常，并且必须在程序中对异常进行处理，否则编译无法通过。

使用**throws**关键字抛出异常的语法格式如下：

```java
修饰符 返回值类型 方法名(参数1,参数2, ...)throws 异常类1,异常类2, ...{
方法体
}
```

***throws**写在方法声明的后面，**throws**后面还需要声明方法中发生异常的类型*

案例演示

```java
public static void main(Sting[] args){
	int result = divide(4,2);//调用方法
	System.out.println(result);
}

//实现两个整数相除，并使用throws声明抛出异常
public static int divide(int x,int y) throws Exception{
	int z = x / y;
	return z;
}
/*运行结果：
未报告的异常错误java.lang.Exception;必须对其进行捕获或声明以便抛出*/
```

*使用**try....catch**处理方法抛出异常*

```java
public static void main(Sting[] args){
try{
	int result = divide(4,2);
	System.out.println(result);
}catch(Exception e){
//打印捕获的异常信息
	e.printStackTrace();
}
public static int divide(int x,int y) throws Exception{
	int z = x / y;
	return z;
}
//运行结果：2
```

​	*注意：使用**throws**抛出异常时，如果程序发生了异常，并且上一层的调用者也无法处理异常时，那么异常会继续被向上抛出，最终直到系统接收到异常，终止程序执行*

现在将**divide()**方法抛出的异常继续抛出

```java
public static void main(Sting[] args)throws Exception{
	int result = divide(4,0);
	System.out.println(result);
}
public static int divide(int x,int y) throws Exception{
	int z = x / y;
	return z;
}
//运行结果：Exception in thread "main" java.lang.ArithmeticException
```

*程序虽然可以通过编译，但在运行时期由于没有对"/by zero"的异常进行处理，最终导致程序终止运行。*

#### 5.34***throw***

与**throws**关键字不同，**throw**用于方法体内，抛出的是一个异常实例，并且每次只抛出一个异常实例

使用**throw**关键字抛出异常的语法格式如下：

```java
throw ExceptionInstance;
```

​	*在方法中，通过**throw**抛出异常后，还需要使用**throws**或**try...catch**对异常进行处理，如果**throw**抛出的**error**、**RuntimeException**或它们的子类异常对象，则无需使用**throws**或**try...catch**对异常进行处理*

案例演示

定义一个**printAge()**输出年龄

```java
void printAge(int age)throws Exception{
if(age <= 0){
//对业务逻辑进行判断，当输入年龄不是正数时抛出异常
	throw new Exception("输入的年龄有误！");
}else{
	System.out.println("此人年龄为:" + age);
	}
}
```

在**main**方法中定义**try...catch**捕获异常

```java
public static void main(Sting[] args){
	int age = -1;
	try{
		printAge(age);
	}catch(Exception e){
		System.out.println("捕获的异常信息为:" + e.getMessage());
	}
}
/*运行结果：
捕获的异常信息为：输入的年龄有误！*/
```



### 5.4自定义异常类

自定义异常类的实例代码如下：

```java
public class MyException extends Exception{
	public MyException(){
	//调用Exception无参的构造方法
	super();
	}
	public MyException(String message){
	//调用Exception有参的构造方法
	super(message);
	}
}
```

​	*若没有特殊的要求，自定义异常类只需继承**Exception**，在构造方法中使用**super()**语句调用**Exception**的构造方法即可*

使用自定义异常类，需要用到**throw**关键字

案例演示

*修改上面的**divide()**方法，在方法中判断被除数是否为负数，如果为负数，就使用**throw**在方法中向调用者抛出自定义的异常对象*

```java
//创建一个自定义异常类
public class MyException extends Exception{
	public MyException(){
	super();
	}
	public MyException(String message){
	super(message);
	}
}
public static void main(Sting[] args){ 
    int a = 10;
    int b = -5;
    try{
        int c = divide(a,b);
        System.out.println("a divide b is " + c );
    }catch(MyException e){
          System.out.println(e.getMessage());
    }
}
//需要在divide()方法上使用throws声明该方法抛出MyException异常
public static int divide(int x,int y) throws MyException{
	if(y < 0){
	throw new MyException("除数是负数");
	}
	int z = x / y;
	return z;
}//运行结果：除数是负数
```





------



## 6.关于图形用户界面

***Swing***组件通常称作“轻量级组件”，它完全由***Java***编写，不依赖操作系统语言

### 6.1***JFrame***

***JFrame***是一个容器，是各个组件的载体

**构造方法**	

```java
*JFrame() 创建没有标题窗口*

*JFrame(String s)创建标题为s的窗口*
```

**常用方法**

```java
*public void setTitle(String title) 设置窗口标题*

*public void setSize(int width,int height) 设置窗口的大小*

*public void setLocation(int x,int y)设置窗口的位置，默认位置(0,0)*

*public void setBounds(int x,int y,int width,int height)设置窗口的初始位置(x,y)和窗口宽width，高height*

*public void setVisible(boolean b)设置窗口是否可见，默认是false*

*public void setResizable(boolean b)设置窗口是否可调整大小，默认是true*

*public void dispose()撤销当前窗口，并释放当前窗口所使用的资源*

*public void setExtendedState(int state)设置窗口的扩展状态，其中参数取JFrame类中的下列类常量*

*MAXIMIZED_HORIZ(水平方向最大化)*

*MAXIMIZED_VERT(垂直方向最大化)*

*MAXIMIZED_BOTH(水平、垂直方向都最大化)*
```

**设置JFrame关闭方式**

```java
*public void setDefaultCloseOperation(int operation)设置单击窗体右上角的关闭图标后，程序会做出怎样的处理：*

*DO_NOTHING_ON_CLOSE(什么也不做)*

*HIDE_ON_CLOSE(隐藏当前窗口)*

*DISPOSE_ON_CLOSE(隐藏当前窗口，并释放窗体占有的其他资源)*

*EXIT_ON_CLOSE(结束窗口所在的应用程序)*
```

**其他方法**

```java
*add()*添加组件·

​	若只把组件传入，就会按照默认布局BorderLayout进行摆放，可以同时传入组件和布局方式。

​	常用布局方式：

​	1.BorderLayout()边界布局（默认布局管理器），参数里可以写入SOUTH,NORTH,EAST,WEST,CENTER

​	2.FlowLayout()流式布局（默认在居中位置，也可以手动修改其位置，例如 new FlowLayout(FlowLayout.LEFT)改为居中对齐）

​	3.GridLayout()网格布局，可以传入指定的行和列

*setLayout()*设置布局方式，默认是边界布局，在参数中传入null会清空布局管理器，组件会按照x、y的位置来摆放，添加组件时需要先调用			隐藏容器 getContentPane()，再使用add()方法

*setLocationRelativeTo(null)* 使界面居中(建议在设置完边界大小后写)

*getContentPane()* 获取隐藏容器(用于添加含有图标的中间容器)

*setAlwaysOnTop(true)*设置界面置顶

*setModal(true)*将对话框设置为标准型（在没被关闭之前不可以进行其他操作）

//注意：当该类继承了JFrame后，直接使用JFrame提供的方法即可，不需要实例化对象再用对象调用方法。
```



### 6.2***JDialog***

它是从一个窗体弹出来的另一个窗体，与***JFrame***相似

**构造方法**

```java
*JDialog()*

*JDialog(Frame f)指定父窗口*

*JDialog(Frame f,String title)指定父窗口 + 标题*
```

**常用方法**

与***JFrame***相似，但设置关闭方式时没有***EXIT_ON_CLOSE***(结束窗口所在的应用程序)。

### 6.3***JPanel***

面板是容器的一种，它可以作为容器，添加容纳其他的组件，**JPanel**是一种最简单的面板。

构造方法

```java
JPanel jPanel1 = new JPanel();//无参构造
JPanel jPanel2 = new JPanel(new FlowLayout());//设置布局方式（默认是流布局）
```

常用方法

```java
add(组件);//添加组件
setBorder(null);//取消边框
setBackground(null);//设置无背景
setOpaque(false);//设置组件不透明为false,即组件透明
```

案例演示

```java
JFrame jf = new JFrame();
jf.setBounds(400,300,1200,1200);
JButton jb1 = new JButton("按钮1");
JButton jb2 = new JButton("按钮2");
//生成一个面板
//括号中可以不传参数或者传入一种布局方式
JPanel jp = new JPanel();
jp.add(jb1);
jp.add(jb2);
jf.add(jp);
jf.setVisible(true);
```



#### 6.31**JScrollPane**

***JScrollPane***是带滚动条的面板,一般和文本域***JTextArea***捆绑使用。***JScrollPane***内只能添加一个组件，建议在创建其对象的时候就把组件作为参数传入，因此如果需要添加多个组件到一个***JScrollPane***中时，需要先将需要添加的组件添加到***JPanel***中，再将***JPanel***添加到***JScrollPane***。

```java
JFrame jf = new JFrame();
jf.setBounds(400,300,1200,200);
JTextArea ja = new JTextArea(30,10);
JScrollPane jp = new JScrollPane(ja);
jf.add(jp);
jf.setVisible();
```

### 6.4***JLabel***

***JLabel***是一种标签组件，显示文本或提示信息，其默认的布局管理器是***FlowLayout()***

**构造方法**

```java
new JLabel();

new JLabel(Icon icon)//设置图标

new JLabel(Icon icon,int aligment)//设置图标 + 水平对齐方式

new JLabel(String str,int aligment)//设置文本 + 水平对齐方式

new JLabel(String str,Icon icon,int aligment)//设置文本 + 图标 + 水平对齐方式
```

**常用方法**

```java
*setText(String s)*重置标签内容

*setToolTipText(String s)*设置鼠标悬停提示
```



### 6.5***JButton***

**JButton**是经典按钮，每个**JButton**之间相互独立

**构造方法**

```java
new JButton();

new JButton(String text);//指定文字

new JButton(Icon icon);//指定图标

new JButton(String text,Icon icon);//指定文字 + 指定图标
```

**其他方法**

```java
setTooltipText(String text)//设置提示文字

setBorderPainted();//设置边界是否显示(默认是true)

setEnabled();//设置按钮是否可用(默认是true)

reset.setContentAreaFilled(false);//设置按钮透明
        
reset.setBorder(null);//取消边框
```

演示

```java
JFrame jf = new JFrame();
//改变布局方式为流布局(默认布局为网格布局)
jf.setLayout(new FlowLayout());
jf.setBounds(400,300,200,300);
JButton jb = new JButton("按钮1");
jb.setEnabled(true);
jf.add(jb);
jf.setVisible(true);
jf.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
```

### 6.6***JRadioButton***

单选按钮。构造方法和***JButton***相同。一般需要需要配合***ButtonGroup***使用

#### 6.61***ButtonGroup***

使单选按钮成组。

**构造方法**

```java
ButtonGroup buttonGroup = new ButtonGroup();
```

**常用方法**

```java
*add(单选按钮对象) *添加单选按钮，所有被添加的单选按钮成组*

*remove(单选按钮) *将指定按钮在组中移除*
```

**案例演示**

```java
ButtonGroup bg = new ButtonGroup();
//创建4个单选按钮
JRadioButton A = new JRadioButton("A");
JRadioButton B = new JRadioButton("B");
JRadioButton C = new JRadioButton("C");
JRadioButton D = new JRadioButton("D");
//将单选按钮成组
bg.add(A);
bg.add(B);
bg.add(C);
bg.add(D);
//将单选按钮放入界面中
jframe.add(A);
jframe.add(B);
jframe.add(C);
jframe.add(D);
//运行时，A、B、C、D按钮只能选其一
```

### 6.7***JCheckBox***

复选框，用来进行选择和非选择两种状态。与单选按钮不同，选项之间互不影响。

**构造方法**

```Java
JCheckBox jb1 = new JCheckBox("1");//参数传入复选框的提示内容
```

**常用方法**

```java
public boolean isSelect() *用于返回复选框的状态。如果复选框被选中返回*true*，否则返回*false*
```



### 6.8***JComboBox***

下拉列表框

**构造方法**

```java
JComboBox jCombobox = new JComboBox<>();//创建一个空的combobox对象
JComboBox jCombobox = new JComboBox<>(ComboBoxModel aModel);//创建一个combobox，其选项选取一个已有的ComboBoxModel
JComboBox jCombobox = new JComboBox<>(Object[] items);//创建包含指定数组中元素的combobox
```

**常用方法**

```java
*addItem(Object anObject)  *将指定的对象作为选项添加到下拉列表框中*
*insertItem(Object anObject, int index) *在下拉列表框中的指定索引处插入项*
*removeItem(Object anObject) *在下拉列表框中删除指定的对象项*
*removeItemAt(int anIndex) *在下拉列表框中删除指定位置的对象项*
*removeAllItem() *从下拉列表框中删除所有项*
*getItemCount() *返回下拉列表框中的项数*
*getSelectededIndex() *获取当前选择的索引*
*getSelectedItem() *获取当前选择的项*
```

**案例分析**

```java
//将下列数组作为下拉列表框的选项
String[] arr = {"Java", "C", "Python"}; 
JComboBox jCombobox = new JComboBox<>(arr);
//做出选择后，可以通过返回的索引确定选择的元素
int index = jCombobox.getSelectededIndex();
//0 -> Java | 1 -> C | 2 -> Python
```



### 6.9***JTextFied***

单行文本框

**构造方法**

```java
*new JTextField()*,创建默认文本框

*new JTextField(int columns)*,创建文本框并设定可以显示的列数

*new JTextField(String text)*,创建文本框并指定内容

*new JTextField(String text, int columns)*,指定内容并设定可以显示的列数
```



**常用方法**

```java
*getText()*获取JTextField内容

*getColumns()*返回文本域的列数

*setText(String s)*修改JTextField内容

*setEnabled(boolean b)*设置是否可编辑

*setEditable(boolean b)*设置文本是否为只读状态

*setToolTipText(String s)*设置鼠标悬停提示

*setForeground(颜色)*设置字体颜色

*setBackground(颜色)*设置文本域颜色
```

另外，还可以设置文本字体的格式，需要用到***Font***类

#### 6.91***Font***

```java
//参数1：字体；参数2：字体加粗/斜体；参数3：字号
Font f1 = new Font("宋体", 0, 16);//正常字体
Font f2 = new Font("宋体", Font.ITALIC, 16);//斜体
Font f3 = new Font("宋体", Font.BOLD, 16);//加粗体
Font f3 = new Font("宋体",Font.ITALIC + Font.BOLD, 16);//加粗斜体
```

给文本设置字体

```java
jTextfield.setFont(f1);
```

可以用相同的方法给***JLabel***、***JButton***等组件设置字体格式

### 6.10***JTextArea***

多行文本框，与***JTextField***相似。使用时一般放入***JScrollPane***中。

**构造方法**

```java
//空参构造
public JTextArea();
//设置内容
public JTextArea(String text);
//设置行列
public JTextArea(int rows, int columns);
//同时设置内容和行列
public JTextArea(String text, int rows, int columns);
```

**常用方法**

```java
*setText(String s)*重置内容

*append(String s)*添加内容

*getText()*获取当前文本域的文本，返回的是一个字符串
```



### 6.11***JMenuBar***

***JFrame***的菜单栏。

**构造方法**

```java
JMenuBar jMenuBar = new JMenuBar();//无形参
```

菜单栏下的条目叫做JMenu

```java
JMenu jMenu = new JMenu(条目名);//括号传入条目名
```

还可以给菜单栏下的条目设置二级条目，叫做***JMenuItem***

```java
JMenuItem jMenuItem = new JMenuItem(二级条目名);
```

**常用方法**

```java
jMenu.add(jMenuItem);//将二级条目添加给一级条目
jMenuBar.add(jMenu);//把一级条目添加给菜单
jFrame.setJMenuBar(jMenuBar);//把菜单添加到主界面
```



### 6.12绑定事件监听

只有当可以交互的组件绑定了事件监听后，才可以执行对应的操作。

#### 6.121***ActionListener***

动作监听。实现按钮按下后执行的方法。

若该方法只执行一次，可以采用匿名内部类的写法。

```java
JButton jButton = new Jbutton("1");
jFrame.add(jButton);
jButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                //点入点击按钮时执行的方法
                System.out.println(e.getActionCommand() + "被点击了");
                //e.getActionCommand()获取调用者，返回类型为字符串
            }
        });
    }
```

注意：***getSource()***得到的组件的名称，而***getActionCommand***得到的是标签(字符串)

可以采取***Lambda***表达式对其进行简化

```java
jButton.addActionListener(e -> System.out.println(e.getActionCommand() + "被点击了"));
```

若该方法多次执行，且点击不同按钮实现的功能不同，可以让该类作为***ActionListener***的实现类，直接在类中重写抽象方法

```java
public class TestDemo implements ActionListener {
    public TestDemo(){
            JFrame jFrame = new JFrame();
		JButton jButton1 = new Jbutton("1");
		JButton jButton2 = new Jbutton("2");
		jFrame.add(jButton1);
		jFrame.add(jButton2);
		jButton1.addActionListener(this);
  	  jButton2.addActionListener(this);
    }
     @Override
    public void actionPerformed(ActionEvent e) {
        //e.getSource()获得目前事件的事件源
        Object obj = e.getSource();
        if(obj == jButton1){
            System.out.println("1被点击了");
        }else if(obj == jButton2){
            System.out.println("2被点击了");
        }
    }
}

```

#### 6.122***ItemListener***

项目监听。

```java
//需要重写该方法
@Override
public void itemStateChanged(ItemEvent e) {

}
```

在对单选按钮添加该方法时，选中时和取消选择都会触发一次项目监听。使用***isSelected()***方法可以判断只有在选中时才执行

#### 6.123***MouseListener***

监听鼠标事件

需要重写以下方法

```java
@Override
public void mouseClicked(MouseEvent e) {
    //鼠标点击（单或双）
}

@Override
public void mousePressed(MouseEvent e) {
	//鼠标按下
}

@Override
public void mouseReleased(MouseEvent e) {
	//鼠标松开
}

@Override
public void mouseEntered(MouseEvent e) {
	//鼠标划入（某组件区域）
}

@Override
public void mouseExited(MouseEvent e) {
	//鼠标划出（某组件区域）
}
```

**常用方法**

```java
int getClickCount()      //得到点击次数1 或 2
int getX(), int getY()   //得到鼠标当前的位置
```

#### 6.124***MouseMotionListener***

对于鼠标的移动和拖放，另外用鼠标运动监听器***MouseMotionListener***。因为许多程序不需要监听鼠标运动，把两者分开可简化程序。

需要重写以下方法

```java
@Override
public void mouseDragged(MouseEvent e) {
	//鼠标拖放
}

@Override
public void mouseMoved(MouseEvent e) {
	//鼠标移动
}
```





------



## 7.关于文件类***File***

**File**类在包**java.io.File**下，代表操作系统的文件对象（文件或文件夹）。创建对象定位文件，可以删除、获取文件信息等，但是不能读写文件内容。**File**对象表示一个路径，可以是文件的路径，也可以是文件夹的路径。这个路径可以是存在的，也允许是不存在的。

**构造方法**

```java
//1.根据文件路径创建对象
String str = "C:\\a.txt";//可以使用单斜杠"/"或者双反斜杠"\\"
File f1 = new File(str);
System.out.println(f1);//C:\Users\name\Desktop\a.txt
//2.根据父路径名字符串和子路径名字符串创建对象
//父路径:C:
//子路径：a.txt
String parent = "C:";
String child = "a.txt";
File f2 = new File(parent,child);
System.out.println(f2);//C:\a.txt
//3.把一个File对象表示的路径和String表示的路径进行拼接
File parent2 = new File("C:");
String child2 = "a.txt";
File f3 = new File(parent2,child2);
```

*注意： 文件路径可以输入绝对路径或相对路径*

**成员方法**

```java
//判断
public boolean isDirectory() *判断此路径名表示的File是否为文件夹*
public boolean isFile() *判断此路径名表示的File是否为文件*
public boolean exist() *判断此路径名表示的File是否存在*
//获取
public long length() *返回文件的大小（字节数量）*
public Sting getAbsolutePath() *返回文件的绝对路径*
public String getPath() *返回定义文件时使用的路径*
public String getName() *返回文件的名称、带后缀*
public long lastModified() *返回文件的最后修改时间*
//创建
public boolean createNewFile() *创建一个新的空的文件*
public boolean mkdir() *创建单级文件夹*
public boolean mkdirs() *创建多级文件夹*
//删除
public boolean delete() *删除文件、空文件夹*
//获取并遍历
public File[] listFiles() *获取当前路径下的所有内容*
public static File[] listRoots() *列出可用的文件系统根（盘符）*
public String[] list *获取当前路径下的所有内容（只获取到文件+后缀名）*
```

注意：1.***length()*** 返回文件的大小（字节数量），这个方法只能获取文件的大小（无法获取文件夹的大小），如果我们需要的单位是			*M,G，可以除以1024*

​			2.***delete()***默认只能删除文件和空文件夹，***delete***方法直接删除不走回收站

​			3.***createNewFile()***如果当前路径表示的文件是不存在的，则创建成功，返回***true***，否则创建失败，返回***false***。如果父级路径是不			存在的，方法会有异常。该方法创建的一定是文件，如果路径中不包括后缀名，则创建一个没有后缀的文件

​			4.***listFiles()***当调用者***File***表示的路径不存在时，返回***null***；当调用者***File***表示的路径是文件时，返回***null***；当调用者File表示的路径			是一个空文件夹时，返回一个长度为0的数组；当调用者***File***表示的路径是一个有内容的文件夹时，将里面所有文件和文件夹的路			径放在***File***数组中返回；当调用者***File***表示的路径是需要权限才能访问的文件夹时，返回***null***

假如***File***对象代表目录，并且目录下包含子目录或者文件，需要使用递归的方式将整个目录以及目录中的文件全部删除

**案例分析**

```java
//创建递归方法deleteDir()，遍历所有的子目录和文件，进行递归删除
public static void deleteDir(File dir) {
    if(dir.exist){//判断传入的File对象是否存在
        File[] files = dir.listFiles();//遍历所有的子目录和文件
        for(File file : files) {//遍历所有的子目录和文件
            if(file.isDirectory()) {
                deleteDir(file);//如果是目录，递归调用deleteDir()
            } else {
                //如果是文件，直接删除
                file.delete();
            }
        }
        //删除完一个目录里的所有文件后，就删除这个目录
        dir.delete;
    }
}
```



------



## 8.关于***IO***流

**·** **I**表示***input***，是数据从硬盘文件读入到内存的过程，称之输入，负责读;

**·** **O**表示***output***，是内存程序的数据从内存到写出到硬盘文件的过程，称之输出，负责写。

从流的方向可以将IO流分为输入流（读取）和输出流（写出）;

从操作文件类型可以将IO流分为字节流（所有类型的文件）和字符流（纯文本文件）。

**案例分析**

字节流： 二进制I/O程序 一个字节被读/写 **123** <-> 文件中写入**01111011**

字符流： 文本I/O程序 字符的Unicode码 **“123”** <-> 字符的编码保存在文件中 **00110001 00110010 00110011**（三个独立的字符对应相应的编码）



**四个顶层抽象类**

|          |    字节流    | 字符流 |
| :------: | :----------: | :----: |
| **输入** | InputStream  | Reader |
| **输出** | OutputStream | Writer |



**四个顶层类实现功能时分成节点流和处理流**

**·**  节点流： (***Node Stream***）：直接与节点（如文件）相连

**·** 处理流：（***Processing Stream***） 对节点流或其他处理流进一步进行处理



### 8.1节点流

重点掌握访问文件（**FileInputStream**、**FileOutputStream**、**FileReader**、**FileWriter**）

*注意：为了防止发生文件找不到异常(**FileNotFoundException**)或IO流异常(**IOException**)，包含流的代码可以写在**try-catch**语句中，最后在**finally**语句中关闭输入输出流，或在使用**throws**声明抛出异常*

#### 8.11***FileInputStream***

**构造方法**

```java
FileInputStream fileInputStream = new FileInputStream(File file);//传入File类
FileInputStream fileInputStream = new FileInputStream(String name);//传入路径字符串
```

**常用方法**

```java
int read() *读一个字节的内容*
int read(byte[] b ) *传入一个字节数组，可以一次性读入几个字节*
int read(byte[] b, int off, int len) *一次性读几个字节，从第几索引（按照字节排序）开始读入，读入的长度*
```

**案例分析**

```java
InputStream fis = new FileInputStream("C:/" + "text.txt");//txt中写入了Java字节流
int b;
while((b = fis.read())!= -1){
/*每读到一个字节的内容存入int中（由于read中不传参，所以只使用int最后的字节内容），如果读到的字节数为-1，就代表文件结束*/
System.out.print((char)b);//强制类型转换为字符再输出
}//Javaå  è  æµ
```

注意：中文字符在存储时占两个字节（假定为2），由于编码类型发生变化，输出时会把两个把字节按照两个字符进行输出就会发生乱码

**解决方法：**

**I.将读入单位变成字节数组**

```java
InputStream fis = new FileInputStream("C:/" + "text.txt");//txt中写入了Java字节流
byte[] buffer = new byte[1024];//相当于存储1k，一般都使用1k做缓存
int len ;
while((len = fis.read(buffer))!= -1){
//这种方法输出需要转换为字符串输出（后两个参数要指明开始索引和读入长度，否则会把整一个1k缓存数组进行输出）
	System.out.print(new String(buffer,0,len));
	}
}//Java字节流
```

**II.将读入单位变成整个文件**

```java
InputStream fis = new FileInputStream("C:/" + "text.txt");//txt中写入了Java字节流
//读取全部字节数组
byte[] buffer = fis.readAllBytes();
//文本内容较少时，不建议使用该方法
System.out.print(new String(buffer));//Java字节流
```



#### 8.12***FileOutputStream***

**构造方法**

```java
OutputStream outputStream = new FileOutputStream(String name);//传入路径字符串
OutputStream outputStream = new FileOutputStream(String name, boolean append);//传入路径字符串+是否能追加内容(默认否)
OutputStream outputStream = new FileOutputStream(File file);//传入File类
OutputStream outputStream = new FileOutputStream(File file, boolean append);//传入File类+是否能追加内容(默认否)
```

**常用方法**

```java
*write(int b) *写一个字节*
*write(byte[] b) *写一个字节数组*
*write(bute[] b, int off, int len) *写一个字节数组的一部分，off表示从这个索引开始，长度为len*
*flush() *写出数据*
*close() *关闭流 如果在 write()后面没有flush()，会先执行一次写出数据的操作*
```



```java
String filepath = "C:\\";
OutputStream fos = new FileOutputStream(filepath + "out.txt");
fos.write('a');//写出单位：字节
fos.write(98);//输出98对应的ASCII码 -> b
fos.flush();//写出数据：ab
byte[] buffer = "Java字节流".getBytes();
fos.write(buffer);//写出单位：字节 -> abJava字节流
fos.close();//关闭流（如果在write()后面没有flush()，会先调用一次flush()）
```

```java
//追加数据
OutputStream ofs = new FileOutputStream(filepath + "out.txt",true);
//true代表允许追加,否则后续写入的内容将会覆盖之前的内容
byte[] buffer = "FileOutputStream".getBytes();
ofs.write(buffer);
ofs.write("\r\n".getBytes());//换行
ofs.flush();
//输出部分内容
byte[] bytes = "和FileInputStream".getBytes();
ofs.write(bytes,1,15);
ofs.close();
/*abJava字节流
FileInputStream*/
```

注意：***getBytes()***方法将字符串编码为 ***byte*** 序列，并将结果存储到一个新的 ***byte*** 数组中

**构造方法**

```java
*getBytes() *使用平台的默认字符集将字符串编码为 byte 序列*
*getBytes(String charsetName) *使用指定的字符集将字符串编码为 byte 序列*
/*可传入"UTF-8, GBK, GB2312"
其中，使用UTF-8的单个汉字的编码长度为3;
使用GBK的单个汉字的编码长度为2;
使用GB2312的单个汉字的编码长度为2*/
```



#### 8.13***FileReader***

以字符为读入单位：

```java
String filepath = "C:\\";
Reader fr = new FileReader(filepath + "data.txt");//txt中写入了Java字符流
int code;
while((code = fr.read())!= -1){
	System.out.print((char)code);//Java字符流
}
```

以字符数组为读入单位：

```java
Reader fr = new FileReader(filepath + "data.txt");//txt中写入了Java字符流
char[] buffer = new char[1024];
int len;
while((len = fr.read(buffer))!= -1){
	String str = new String(buffer,0,len);
	System.out.print(str);//Java字符流
}//Java字符流
```



#### 8.14***FileWriter***

```java
Writer fw = new FileWriter(filepath + "out.txt",true);//追加
fw.write('a');
fw.write(98);
fw.write("Java");
fw.write("\r\n");
char[] chars = "文件字符输出流".toCharArray();
fw.write(chars);
fw.close();
/*abJava
文件字符输出流*/
```



### 8.2处理流

重点掌握缓冲流（***BufferedInputStream***、***BufferedOutputStream***、***BufferedReader***、***BufferedWriter***）



#### 8.21***BufferedInputStream***

**构造方法**

```java
//括号内传入要包装的字节输入流和缓冲大小 
BufferedInputStream bufi = new BufferedInputStream(FileInputStream fis,byte b);
```

**常用方法**

```java
public int read()//读入数据
public void close()//关闭流
public int available() //返回可读入的字节数
public long skip(long n)//跳过输入流上的n个字节
public boolean markSupported()//判断该输入流是否支持mark和reset方法
public void mark(int readlimit)//在输入流的当前位置做标记
public void reset()//把流重新定在上一次标记的位置
```

**综合案例演示**

```java
String filename = "C:/text.txt";//txt写入This is a very long text.
	try{
		FileInputStream in = new FileInputStream(filename);
         BufferedInputStream bufi = new BufferedInputStream(in,1024);//缓冲1k
         System.out.println(bufi.available());//available返回可读入的字节数：25（空格、字母占一个字节）
         int half = bufi.available() / 2; //12
         bufi.skip(half);
         if(bufi.markSupported()) {
		int limit;
		limit = bufi.available();
		System.out.println(limit);//13
		bufi.mark(limit);
		for (int i = 0; i < limit; i++)
			System.out.print((char) (bufi.read()));//ry long text.
		System.out.println();
		bufi.reset();
		}
		int c;
		while((c = bufi.read())>= 0)
			System.out.print((char)c);//ry long text.
		bufi.close();
	}catch(IOException e){
		e.printStackTrace();
}
```



#### 8.22***BufferedOutputStream***

```java
String filename = "C:/out.txt";
	try{
		FileOutputStream out = new FileOutputStream(filename,false);
		BufferedOutputStream bufo = new BufferedOutputStream(out);
		String s = "Hello Java World.\r\n";
         byte[] ob = s.getBytes();
         for(int i = 0; i < 10; i++)
			bufo.write(ob,0,ob.length);//将一个字节数组中的部分数据写到缓冲输出流中
		bufo.flush();//清空缓冲输出流，将缓冲区中的所有内容强行写到基层的节点流中
         bufo.close();
	} catch(IOException e){
		e.printStackTrace();
	}
}//out.txt写入10次Hello Java World.
```



#### 8.23***BufferedReader && BufferedWriter***

**综合案例分析**

```java
//定义一个方法：复制一个文本的内容到另一个文本
static void copy(String source, String dest){
	try{//缓冲输入流定义
		FileReader fr = new FileReader(source);//输入流
		BufferedReader br = new BufferedReader(fr);//缓冲输入流(可以不指定缓冲大小)
		//缓冲输出流定义
		FileWriter fw = new FileWriter(dest);//输出流
		BufferedReader bw = new BufferedReader(fw);//缓冲输出流
		String s;
		while((s = br.readLine())!= null){
		//readLine()方法从文件中读入一行数据(只有所有数据读取完才返回null，不用担心两行话中间插空隔开时会提前返回null)
			bw.write(s);
			bw.newLine();//加行标志(防止写入内容堆在同一行)
		}
    	bw.flush();
   		bw.close();
    	fw.close();
   		br.close();
    	fr.close();
	}catch(IOException e){
    	 e.printStackTrace();
	}
}
public static void main(String[] args){
    String path = "C:/";
    String sourceName = path + "bufferin.txt";//bufferin.txt写入Java处理流
	String destName = path + "bufferout.txt";//bufferout.txt为空
    copy(sourceName,destName);//bufferout.txt写入Java处理流
}
```


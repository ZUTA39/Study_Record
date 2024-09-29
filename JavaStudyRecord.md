# Java 学习记录

由于已经有C，C++，Python基础，所以对于基础语法我们一笔带过，主要记录类与对象之后的内容。

## 前情提要

### 关于类型

- Java中对于字符串有专门的**类**：String（一定大写），定义对象（或者说是变量）和一般的类方法一样。
- 如果想要转换数据类型，有两种方法：
    1.直接向这个变量前加"(类型名)"：

    ```java
       //eg.（int变double）
            double n = (double)a;
    ```

    2.利用专门的方法：

    ```java
    int num = Integer.parseInt(s1);
    double num = Double.parseDouble(s1);
    float num = Float.parseFloat(s1);
    long num = Long.parseLong(s1);
            
    ```

    所谓Integer等等，即是int等类型对应的包裹类型，用于将基本数据类型（如 int、double 等）包装成对象。

    ```text
        int 对应 Integer
        double 对应 Double
        float 对应 Float
        long 对应 Long
        char 对应 Character
        boolean 对应 Boolean
        byte 对应 Byte
        short 对应 Short
    ```

    包裹类型的主要用途包括：

  - 对象存储：基本数据类型不能直接存储在集合类（如 ArrayList、HashMap）中，而包裹类型可以。
  - 类型转换：提供了将字符串转换为相应的基本数据类型的方法，例如 Integer.parseInt(String)。
  - 提供常用方法：包裹类型提供了许多实用方法，例如 Integer 类的 compareTo 方法、Double 类的 isNaN 方法等。

### 控制精度

使用String类的format方法来控制精度（实际上会四舍五入）

```java
double space = PI * pow(radius, 2) * angle/360;
String formatspace = String.format("%.6f", space);
```

如果只想直接去掉小数点之后的数字，那么就可以直接将浮点数转换为整数

```java
num = 3.5867422; // 如果用上面的方法，结果就是4
num = Math.floor(num) // 这样就是3
```

### Math类常用的方法与属性

#### 方法

- 绝对值：

```java
Math.abs(-10); // 返回 10
```

- 最大值和最小值：

```java
Math.max(5, 10); // 返回 10
Math.min(5, 10); // 返回 5
```

- 幂运算：

```java
Math.pow(2, 3); // 返回 8.0
```

- 平方根：

```java
Math.sqrt(16); // 返回 4.0
```

- 三角函数：

```java
Math.sin(Math.PI / 2); // 返回 1.0
Math.cos(0); // 返回 1.0
Math.tan(Math.PI / 4); // 返回 1.0
```

- 对数：

```java
Math.log(1); // 返回 0.0 (自然对数)
Math.log10(100); // 返回 2.0 (以10为底的对数)
```

- 取整：

```java
Math.ceil(2.3); // 返回 3.0 (向上取整)
Math.floor(2.7); // 返回 2.0 (向下取整)
Math.round(2.5); // 返回 3 (四舍五入)
```

- 随机数：

```java
Math.random(); // 返回一个0.0到1.0之间的随机数
```

#### 属性

```java
Math.PI;// 圆周率常量
Math.E;//自然数底数
```

### 输入

在Java中输入被放到了一个特殊的方法里。

步骤：
1.导入Scanner类所在的包，java.util.*
2.创建该类对象（声明变量）
3.调用里面的功能

```java
improt java.util.* // "*"表示导入包内的所有类

public class Main { // 假设这个程序名称为"Main"
    public static main(String[], args) {
        Scanner scanner = new Scanner(System.in);
        int a = scanner.nextInt();
        int b = scanner.nextInt();
        scanner.close();
    }
}

```

Java的输入比C更为严谨，在安全性方面有较大提升，体现在使用Scanner类输入时需要关闭对象，以释放资源，防止资源泄漏。

须知，Java中也有转义字符，和普通要输出的语句一样需要在双引号里使用

### 数组

1.数组类型[] 数组名 = new 数据类型[大小]

```java
int[] a = new int[5];//创建了一个数组，存放5个int
```

相当于C里的int a[5]

可以通过：

```java
a.length
```

输出数组大小/长度。

2.先声明再创建

```java
int[] b;
b = new int[5];
```

3.数组的赋值与扩容

Java中的数组是用 ***花括号*** 括起来的
之前在C里，数组和数组之间是不能赋值的，现在在Java里可以但是赋的是地址（引用传递），所以赋的那个变了，被赋的也会跟着变。

```java
int[] arr = {1, 2, 3};
int[] arrNew = new int[arr.length+1];
for (int i = 0; i < arr.length; i++) {
    arrNew[i] = arr[i];
}
arrNew[arr.length+1] = 4;
arr = arrNew;
```

### 新增的for-each循环

说是新增，其实在python也见过。就是：对于数组/容器的每一个字符……

```java
int[] a = {1, 2, 3};
for(int element : a) {
    // 省略
}
```

## 类与对象

对于一个事物，想要抽象成类，就要抽象出它的特有的属性特点及可以进行的动作（操作）【即方法】，而我们所定义的新的（new）对象，即为“具体的”一个类。例如狗这个种类和我的狗这一特殊“对象”。

### 定义对象

```java
class Dog {
    String name;
    int age;
    String owner;

    // 函数及以下省略
}

public class Main { // 假设这个程序名称为"Main"
    public static void main(String[], args) {
        my_dog = new Dog;
    }
}
```

对于类，我们可以为其所含有的属性赋初始值，也可以在主类中定义类的对象时传入属性值，这一切都要在类中的**定义方法**进行。

- **赋初始值**
  
    ```java
    //
    class Dog {
        String name;
        int age;
        String owner;

        Dog() {
            this.name = "Bread";
            this.age = 4;
            this.owner = "Bob";
        }

        // 下略
    }
    ```

    this关键字的作用是锁定当前所指的是这个对象中的变量（属性值）

    也不一定非要用定义方法，可以是：

    ```java
    // 赋初始值
    class Dog {
        String name = "Bread";
        int age = 4;
        String owner = "Bob";

        // 下略
    }
    ```

- **在定义新对象时由外部（主类）传入值**

    ```java
    // 
    class Dog {
        String name;
        int age;
        String owner;

        Dog(String name, int age, String owner) {
            this.name = name;
            this.age = age;
            this.owner = owner;
        }

        // 下略
    }
    ```

当然传入参数的名字也不一定非要这么起。

### 类中的函数--方法

类当中的方法即为要进行的操作。
主要注意：

- 改变成员变量（即类自己的属性变量）本身时要加"private"，即这个方法是私有的，以保证其安全性。
  
  ```java
    class Fraction { // 表示分数的类
        int a; // 分子
        int b; // 分母
        int ready; //分数本身

        Fraction(int a, int b) {
            int gcd = gcd(a, b);
            if (gcd != 0) {
                this.a = a / gcd;
                this.b = b / gcd;
            }
            else {
                this.a = a;
                this.b = b;
            }
            this.ready = a / b;
        }

        private int gcd(int a, int b) { // 计算最大公约数
            if (b == 0) {
                return a;
            }
            return gcd(b, a % b);
        }
    }
  ```

## 对象交互

### 类套类的设计

对于一个电子时钟，我们如何将其抽象成一个类？
可以将其看作“小时” + “分钟”的模式，而小时与分钟也有共同点，它们都有一个限制，过了这个限制就会归零。
因此，我们可以定义一个clock类和Display类（用于小时和分钟），而clock类中包含两个Display类（小时和分钟）。

```java
public class clock {
    private Display minitue = new Display(60);
    private Display hour = new Display(24);

    void start() {
        while(true) {
            minitue.increase();
            if(minitue.getValue() == minitue.limit) {
                minitue.value = 0;
                hour.increase();
                if(hour.getValue() == hour.limit) {
                    hour.value = 0;
                }
            }
            System.out.print(hour.value + ":" + minitue.value + "\n");
        }
    } 
    public static void main(String[] args) {
        clock time = new clock();
        time.start();
    }
}

class Display {
    int limit;
    int value = 0;

    Display(int limit) {
        this.limit = limit;
    }

    public void increase() {
        value++;
    }

    public int getValue() {
        return value;
    }
}
```

### 访问属性

封装，就是把 ***数据*** 和对这些数据的 ***操作放在一起*** ，并且用这些操作把数据掩盖起来，是面向对象的最核心概念。

#### 封闭的访问属性--private

- 所有的 ***成员变量*** 必须是private的，这样就避免外部任意使用你的内部数据，只有 ***对象内部*** 可以访问。
- 所有public的函数，只是用来实现这个类的对象或类自己要提供的服务的，而不是用来直接访问数据的。除非对数据的访问就是这个类及对象的服务。简单地说，给每个成员变量提供一对用于读写的get/set函数也是不合适的设计。

**注意**:private是针对类不是针对对象！！所以哪怕在这个类（含private变量）中引用了另一个同样的这个类，也是可以正常访问的

#### 开放的访问属性--public

与之前的private相反，主要用在方法和类上。因此我们这里只针对方法和类讨论。

- 对于方法
如果我们定义的类中的方法前面什么都没有，默认为--friendly，即在 ***同一个包*** 中可以任意使用。

- 对于类
每一个public class都属于一个对应的编译单元（java源文件），换句话说，一个编译单元只能有一个public class。
如果在其他Java源代码中想要使用另一个Java源文件中的内容，就只能访问其public class。

### 包

当你的程序越来越大的时候，你就会需要有一个机制帮助你管理一个工程中众多的类了。包就是Java的类库管理机制，它借助文件系统的目录来管理类库，一个包就是一个目录，一个包内的所有的类必须放在一个目录下，那个目录的名字必须是包的名字。

如果你创建一个包（例如exercise），那么在该包目录下的每个Java文件的开头都应该包含 ***package exercise*** 声明。这样可以确保这些文件都属于同一个包。

包中可以再套包。

### 类变量和类方法

类是描述，对象是实体。在类里所描述的成员变量，位于这个类的每一个对象中的。
而如果某个成员有static关键字做修饰，它就不再属于每一个对象，而是属于整个类的了。

通过每个对象都可以访问到这些类变量和类函数，但是也可以通过类的名字来访问它们。类函数由于不属于任何对象，因此也没有办法建立与调用它们的对象的关系，就不能访问任何非static的成员变量和成员函数了。

#### 类变量

含static的变量即为类变量。
顾名思义，类变量是 ***属于*** 这个类的，对于其每一个对象，这个值是共有的

#### 类方法

含static的方法即为类方法。
类方法的意思是，可以通过类名直接调用，而不需要创建类的实例。

**注意**：类方法中没有 this 关键字，因为类方法不依赖于任何对象实例，而 this 关键字是用于引用当前对象实例的。

## 对象容器

容器是现代程序设计非常基础而重要的手段。

所谓容器，就是“放东西的东西”。数组可以看作是一种容器，但是数组的元素个数一旦确定就无法改变，这在实际使用中是很大的不足。一般意义上的容器，是指具有自动增长容量能力的存放数据的一种数据结构。在面向对象语言中，这种数据结构本身表达为一个对象。所以才有“放东西的东西”的说法。

Java具有丰富的容器，Java的容器具有丰富的功能和良好的性能。熟悉并能充分有效地利用好容器，是现代程序设计的基本能力。

***在一些书中，将容器（英文为collection或container）翻译为“集合”，由于数学中的集合（Set）也是一种特定的容器类型，我们认为将collection翻译为集合是不恰当的。所以我们只会使用容器一词。***

### 顺序容器

#### 举个例子

我们首先学习的是顺序容器，即放进容器中的对象是按照指定的顺序（放的顺序）排列起来的，而且允许具有相同值的多个对象存在。

假设我们现在现在想要写一个程序，实现记事本的功能：

- 能存储记录。
- 不限制存储记录的数量。
- 可以知道已存储记录的数量。
- 能查看每一条存储记录。
- 可以进行删除操作。
- 可以列出所有记录。
  
注意，与初学者不同，我们现在需要思考的是如何设计 ***接口***
何为接口？即处理别人（例如前端网页，命令行，图形界面）传过来的数据。
也就是说，我们需要将人机交互和业务逻辑分离！
返回处理后的数据而不是直接输出！

观察需求，因为需要不限制数量，所以不可以用数组。

***要用容器！！***

容器是个啥？其实是一种 ***类***。这里我们使用ArryList容器类。

#### ArryList定义及所含方法

```java
ArryList<元素类型> 对象名 = new ArryList<元素类型>;
```

ArryList的方法：

- add() / add(location, element) // 插入 / 向location位置插入element（后面的元素会自动向后移，不用管）
- size() // 返回大小
- get(index) // 返回index索引值
- remove(index) // 删除并返回index索引值
- toArray 方法有两个重载版本：
    1.toArray()：将 ArrayList 转换为一个包含所有元素的 Object 数组。
    2.toArray(T[] a)：将 ArrayList 转换为一个包含所有元素的指定类型的数组。如果指定的数组长度不足以容纳所有元素，则会创建一个新的数组。（T[] a 指T类型的数组a，如果之前没定义数组a，这里就需要你新定义数组（在括号里定义就行））

#### 在创建对象容器时，究竟把什么放入了容器？

例如字符串容器就是一种对象容器。

在 Java 中，当我们使用 ArrayList 的 add 方法将对象放入容器时，实际上是将对象的引用放入了容器中，而不是对象本身：

- 放进去的是什么：放进容器的是对象的引用，而不是对象本身。Java 中的对象是通过引用来操作的，ArrayList 存储的是这些引用。
- 对象是否还在外面：放入容器后，原来的对象引用仍然存在于外部。也就是说，外部的引用和容器中的引用都指向同一个对象。
- ***修改对象的影响***：如果修改了放入容器的对象，由于容器中存储的是对象的引用，因此容器中的对象也 ***会反映出*** 这些修改。因为外部引用和容器中的引用指向的是同一个对象。

### 对象数组

#### 以对象为元素的数组？

当数组的元素的类型是类的时候，数组的每一个元素其实只是对象的引用而不是对象本身。因此，仅仅创建数组并没有创建其中的每一个对象！
初始时，数组中的每个元素都是 null，因为还没有为这些引用分配实际的对象。

for-each循环对对象数组仍然适用。

#### 如何设计能传递任意数量参数的函数？

在 Java 中，可以使用可变参数（varargs）来设计能够传递任意数量参数的函数。可变参数允许你在调用方法时传递任意数量的参数，而不需要显式地定义每个参数。可变参数在方法定义中使用省略号（...）表示。

```java
public class VarargsExample {
    public static void main(String[] args) {
        // 调用方法时传递不同数量的参数
        printNumbers(1, 2, 3);
        printNumbers(4, 5);
        printNumbers(6);
        printNumbers(); // 不传递参数
    }

    // 使用可变参数定义方法
    public static void printNumbers(int... numbers) {
        for (int number : numbers) {
            System.out.print(number + " ");
        }
        System.out.println();
    }
}
```

可变参数的使用 ***注意事项*** ：

可变参数必须是方法的最后一个参数。例如，public void exampleMethod(String name, int... numbers) 是合法的，但 public void exampleMethod(int... numbers, String name) 是非法的。
在方法内部，可变参数被当作数组来处理，因此可以使用数组的所有操作。

### 集合容器（set）

#### 集合的概念和特殊的输出

集合就是数学中的集合的概念：所有的元素都具有唯一的值，元素在其中没有顺序。

```java
HashSet<String> a = new HashSet<String>();
a.add("first");
a.add("second");
a.add("first");
System.out.println(a);
```

类似Python，会输出：[first, second]

集合（如 HashSet、TreeSet 等）不支持通过索引获取元素，因为它们没有顺序概念。要获取某个位置上的值，可以使用 List 接口的实现类（如 ArrayList、LinkedList 等），这些类支持通过索引访问元素。

#### 直接输出一整个集合/数组？

在 Java 中，集合类（如 HashSet、ArrayList 等）默认实现了 toString() 方法，因此可以直接使用 System.out.println() 输出集合的内容，而不需要显式调用 toString() 方法。

例如，以下代码：

```java
HashSet<String> a = new HashSet<String>();
a.add("first");
a.add("second");
a.add("first");
System.out.println(a);
```

会输出集合的内容 [first, second]，因为 HashSet 类已经重写了 toString() 方法。

对于数组，必须使用 Arrays.toString() 方法来输出数组的内容，因为 ***数组类没有重写 toString() 方法*** ，直接打印数组会输出其内存地址。例如：

```java
int[] numbers = {1, 2, 3, 4, 5};
System.out.println(numbers); // 输出类似于 [I@1b6d3586
System.out.println(Arrays.toString(numbers)); // 输出 [1, 2, 3, 4, 5]
```

总结：

- 集合类可以直接使用 System.out.println() 输出内容。
- 数组需要使用 Arrays.toString() 方法来输出内容。

### 散列表（Hash）

传统意义上的Hash表，是能以int做值，将数据存放起来的数据结构。Java的Hash表可以以任何实现了hash()函数的类的对象做值来存放对象。

事实上，散列表我们早就不陌生，甚至可以说是熟的不行了。像C++中的map，Python中的字典，都是一种散列表。

举例（硬币对应的名称）：

```java
public class test {
    public static void main(String args[]) {
        Scanner input = new Scanner(System.in);
        int amount = input.nextInt();
        input.close();
        Coin c1 = new Coin();
        System.out.println(c1.getname(amount));
    }
}

class Coin {
    private HashMap<Integer, String> coinnames = new HashMap<Integer, String>();

    public Coin() {
        coinnames.put(1, "penny");
        coinnames.put(10, "dime");
        coinnames.put(25, "quarter");
        coinnames.put(50, "half_dollar");
    }

    public String getname(int amount) {
        return coinnames.get(amount);
    }
}
```

#### HashMap的方法及遍历

- put(amount) //
- get(amount) //
- containsKey(amount) //
- keySet() // 把键整合成一个 ***集合***，有下属方法size()得到有几个元素。注意 ***键是唯一的***。

遍历：

```java
// 仍然沿用上面的例子
for(Integer k : coinnames.keySet()) {
    String s = cionnames.get(k);
    Sysem.out.println(s);
}
```

## 继承与多态

面向对象程序设计语言有三大特性：封装、继承和多态性。继承是面向对象语言的重要特征之一，没有继承的语言只能被称作“使用对象的语言”。继承是非常简单而强大的设计思想，它提供了我们代码重用和程序组织的有力工具。

类是规则，用来制造对象的规则。我们不断地定义类，用定义的类制造一些对象。类定义了对象的属性和行为，就像图纸决定了房子要盖成什么样子。

一张图纸可以盖很多房子，它们都是相同的房子，但是坐落在不同的地方，会有不同的人住在里面。假如现在我们想盖一座新房子，和以前盖的房子很相似，但是稍微有点不同。任何一个建筑师都会拿以前盖的房子的图纸来，稍加修改，成为一张新图纸，然后盖这座新房子。所以一旦我们有了一张设计良好的图纸，我们就可以基于这张图纸设计出很多相似但不完全相同的房子的图纸来。

基于已有的设计创造新的设计，就是面向对象程序设计中的继承。在继承中，新的类不是凭空产生的，而是基于一个已经存在的类而定义出来的。通过继承，新的类自动获得了基础类中所有的成员，包括成员变量和方法，包括各种访问属性的成员，无论是public还是private。当然，在这之后，程序员还可以加入自己的新的成员，包括变量和方法。显然，通过继承来定义新的类，远比从头开始写一个新的类要简单快捷和方便。继承是支持代码重用的重要手段之一。

类这个词有分类的意思，具有相似特性的东西可以归为一类。比如所有的鸟都有一些共同的特性：有翅膀、下蛋等等。鸟的一个子类，比如鸡，具有鸟的所有的特性，同时又有它自己的特性，比如飞不太高等等；而另外一种鸟类，比如鸵鸟，同样也具有鸟类的全部特性，但是又有它自己的明显不同于鸡的特性。

如果我们用程序设计的语言来描述这个鸡和鸵鸟的关系问题，首先有一个类叫做“鸟”，它具有一些成员变量和方法，从而阐述了鸟所应该具有的特征和行为。然后一个“鸡”类可以从这个“鸟”类派生出来，它同样也具有“鸟”类所有的成员变量和方法，然后再加上自己特有的成员变量和方法。无论是从“鸟”那里继承来的变量和方法，还是它自己加上的，都是它的变量和方法。

### 继承

#### 媒体资料库的设计

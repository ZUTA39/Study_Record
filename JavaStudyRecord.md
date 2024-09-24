# Java 学习记录

由于已经有C，C++，Python基础，所以对于基础语法我们一笔带过，主要记录类与对象之后的内容。

## 前情提要

### 关于类型

- Java中对于字符串有专门的**类**：String（一定大写），定义对象（或者说是变量）和一般的类方法一样。
- 如果想要转换数据类型，有两种方法：
    1.直接向这个变量前加"(类型名)"：

    ```java
       //eg.（int变double）
            (double)a;
    ```

    2.利用专门的方法：

    ```java
    int num = Integer.parseInt(s1);
    double num = Double.parseDouble(s1);
    float num = Float.parseFloat(s1);
    long num = Long.parseLong(s1);
            
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

封装，就是把**数据**和对这些数据的**操作***放在一起*，并且用这些操作把数据掩盖起来，是面向对象的最核心概念。

#### 封闭的访问属性--private

- 所有的*成员变量*必须是private的，这样就避免外部任意使用你的内部数据，只有对象内部可以访问。
- 所有public的函数，只是用来实现这个类的对象或类自己要提供的服务的，而不是用来直接访问数据的。除非对数据的访问就是这个类及对象的服务。简单地说，给每个成员变量提供一对用于读写的get/set函数也是不合适的设计。

**注意**:private是针对类不是针对对象！！所以哪怕在这个类（含private变量）中引用了另一个同样的这个类，也是可以正常访问的

#### 开放的访问属性--public

与之前的private相反，主要用在方法和类上。因此我们这里只针对方法和类讨论。

- 对于方法
如果我们定义的类中的方法前面什么都没有，默认为--friendly，即在*同一个包*中可以任意使用。

- 对于类
每一个public class都属于一个对应的编译单元（java源文件），换句话说，一个编译单元只能有一个public class。
如果在其他Java源代码中想要使用另一个Java源文件中的内容，就只能访问其public class。

### 包

当你的程序越来越大的时候，你就会需要有一个机制帮助你管理一个工程中众多的类了。包就是Java的类库管理机制，它借助文件系统的目录来管理类库，一个包就是一个目录，一个包内的所有的类必须放在一个目录下，那个目录的名字必须是包的名字。

如果你创建一个包（例如exercise），那么在该包目录下的每个Java文件的开头都应该包含*package exercise*声明。这样可以确保这些文件都属于同一个包。

包中可以再套包。

### 类变量和类方法

类是描述，对象是实体。在类里所描述的成员变量，位于这个类的每一个对象中的。
而如果某个成员有static关键字做修饰，它就不再属于每一个对象，而是属于整个类的了。

通过每个对象都可以访问到这些类变量和类函数，但是也可以通过类的名字来访问它们。类函数由于不属于任何对象，因此也没有办法建立与调用它们的对象的关系，就不能访问任何非static的成员变量和成员函数了。

#### 类变量

含static的变量即为类变量。
顾名思义，类变量是*属于*这个类的，对于其每一个对象，这个值是共有的

#### 类方法

含static的方法即为类方法。
类方法的意思是，可以通过类名直接调用，而不需要创建类的实例。

**注意**：类方法中没有 this 关键字，因为类方法不依赖于任何对象实例，而 this 关键字是用于引用当前对象实例的。

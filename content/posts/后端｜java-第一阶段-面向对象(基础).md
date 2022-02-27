---
title: "后端｜java-第一阶段-面向对象(基础)"
subtitle: ""
date: 2022-02-27T10:54:15+08:00
draft: false
author: ""
authorLink: ""
description: ""
keywords: ""
license: ""
comment: false
weight: 0

tags:
- Java
categories:
- 有求必应屋

hiddenFromHomePage: false
hiddenFromSearch: false

summary: ""
resources:
- name: featured-image
  src: featured-image.jpg
- name: featured-image-preview
  src: featured-image-preview.jpg

toc:
  enable: true
math:
  enable: false
lightgallery: false
seo:
  images: []

# See details front matter: /theme-documentation-content/#front-matter
---

## 类与对象

### 类与对象关系概述

![](https://tva1.sinaimg.cn/large/e6c9d24egy1gzq0a3p0ruj215t0lfafg.jpg)

### 快速入门

```java

package 面向对象_basic;

// 使用面向对象的方式来解决养猫问题
//
// 定义一个猫类 Cat -> 自定义的数据类型
class Cat {
    //属性
    String name;
    int age;
    String color;
    //行为
}


public class Pre {
    public static void main(String[] args) {

        //使用OOP面向对象解决
        //实例化一只猫[创建一只猫对象]
        //解读
        //1.new Cat() 创建一只猫
        //2. Cat cat1 = new Cat(); 把创建的猫赋给cat1 / Cat是数据类型
        //3. cat1 就是一个对象
        Cat cat1 = new Cat();
        cat1.name = "小白";
        cat1.age = 3;
        cat1.color = "白色";
        //创建第二只猫，并赋给cat2
        //cat2 也是一个对象
        Cat cat2 = new Cat();
        cat2.name = "小花";
        cat2.age = 100;
        cat2.color = "花色";

        //怎么访问对象的属性呢
        System.out.println("第一只猫信息" + cat1.name + " " + cat1.age
                + " " + cat1.color);
        System.out.println("第二只猫信息" + cat2.name + " " + cat2.age
                + " " + cat2.color);
    }
}


```

- 类是抽象的，概念的，代表一类食物，比如人类，猫类.., 即它是数据类型
- 对象是具体的，实际的，代表一个具体事物，即 是实例
- 类是对象的模版，对象是类的一个个体，对应一个实例



### 对象内存布局

```
Cat cat = new Cat();
cat.name = "小白"；
cat.age = 12; 
cat.color = "白色";

```

![](https://tva1.sinaimg.cn/large/e6c9d24egy1gzq0ack7gwj20zg0le0v8.jpg)


### 属性概念

基本介绍

- 从概念或者叫法上看：成员变量 = 属性 = field（字段） （即 成员变量是用来表示属性的，授课中，统一叫 属性）
- 属性是类的一个组成部分，一般是基本数据类型，也可是引用类型（对象，数组），比如我们之前定义猫类的int age就是属性

```java

class Cat {
    //属性
    String name; //成员变量 = 属性 = field（字段）
    int age;
    String color;
    String[] master; //属性可以是基本数据类型，也可以是引用类型
    //行为
}

```



### 属性的注意事项和细节

1.属性的定义语法同变量 示例：访问修饰符 属性类型 属性名;

- 这里老师简单介绍访问修饰符：控制属性的访问范围
- 有四种访问修饰符 public / protected / 默认 / private - 后面会详细介绍 

2.属性的定义类型可以为任意类型，包含基本类型或引用类型

3.属性如果不赋值，有默认值，规则和数组一致

```java

package 面向对象_basic;

public class PropertiesDetail {
    public static void main(String[] args) {
        //创建Person对象
        //p1 是对象名（对象引用）
        //new Person() 创建的对象空间（数据）才是真正的对象
        Person p1 = new Person();

        //对象的属性默认值 遵守数组规则
        System.out.println("\n当前这个人信息");
        System.out.println("age=" + p1.age + " name=" + p1.name + " sal=" + p1.sal +
                " isPass=" + p1.isPass);

    }
}

// 使用面向对象的方式来解决养猫问题
//
// 定义一个猫类 Cat -> 自定义的数据类型
class Person {
    int age;
    String name;
    double sal;
    boolean isPass;
}

// 输出 age=0 name=null sal=0.0 isPass=false
  
```



### 创建对象访问属性

如何创建对象

1.先声明再创建

Cat cat；//声明对象cat

cat = new Cat(); //创建

2.直接创建

Cat cat = new Cat();



### 对象分配机制

![](https://tva1.sinaimg.cn/large/e6c9d24egy1gzfq6o37snj21is0m3dlo.jpg)



### 对象创建过程

Java内存的结构分析

- 栈 - 一般存放基本数据类型 - 局部变量
- 堆 - 存放对象（Cat cat，数组等）
- 方法区：常量池（常量，比如字符串），类加载信息
- 示意图 [Cat(name, age, price)]

![](https://tva1.sinaimg.cn/large/e6c9d24egy1gzfqfs1rubj20x80ckdj2.jpg)



### 对象机制练习

![](https://tva1.sinaimg.cn/large/e6c9d24egy1gzfqnfbt3gj21hs0ma79o.jpg)




## 成员方法



### 方法快速入门

1.基本介绍

- 在某些情况下，我们还需要定义成员方法（简称方法）。比如人类：除了有一些属性外（年龄，姓名...），我们人类还有一些行为比如：可以说话、跑步...，通过学习，还可以做算术题。这时就要用成员方法才能完成。现在要求对Person类完善

2.成员方法快速入门 

```java

package 面向对象_basic;

public class Method01 {
    public static void main(String[] args) {
        //方法使用
        //1 - 方法写好后，如果不去调用（使用），不会输出
        //2 - 先创建对象，然后调用方法即可
        Person p1 = new Person();
        p1.speak();//调用方法
        p1.cal01();//调用cal01方法
        p1.cal02(5);//表示调用cal02方法时，同时给n一个5 n=5
        p1.cal02(10);//表示调用cal02方法时，同时给n一个10 n=10

        //调用了getSum方法，同时num1=10，num2=20
        //把 方法 getSum 返回的值，赋给 变量 returnRes
        int returnRes = p1.getSum(10,20);
        System.out.println("getSum方法返回的值=" + returnRes);
    }
}

class Person {
    int age;
    String name;
    //方法method
    //添加speak 成员方法，输出"我是一个好人"
    //解读
    //1 - public 表示方法是公开的
    //2 - void 表示方法没有返回值
    //3 - speak 方法名，（）形参列表
    //4 - 方法体，可以写我们要执行的代码
    //5 - System.out.println("我是一个好人"); 表示我们方法就是输出一句话
    public void speak() {
        System.out.println("我是一个好人");
    }
    //添加 cal01 成员方法，可以计算从 1+...+1000的结果
    public void cal01() {
        //循环完成
        int res = 0;
        for(int i = 1; i <=1000; i++) {
            res += i;
        }
        System.out.println("cal01计算结果=" + res);
    }
    //添加cal02成员方法，该方法可以接收一个数n，计算从1+..+n的过程
    //解读
    //1 - (int n)形参列表，表示当前有一个形式参数，可以接受用户的输入
    public void cal02(int n) {
        int res = 0;
        for(int i = 1; i <=n; i++) {
            res += i;
        }
        System.out.println("cal02计算结果=" + res);
    }
    //添加getSum成员方法，可以计算两个数的和
    //老韩解读
    //1. public 表示方法是公开的
    //2. int 表示方法执行后，返回一个int值
    //3. getSum 方法名
    //4. (int num1, int num2) 形参列表，2个形参，可以接收用户传入的两个数
    //5. return res; 表示把res值返回
    public int getSum(int num1, int num2) {
        int res = num1 + num2;
        return res;
    }
}

```



### 方法的调用机制原理

画出程序执行过程[getSum] + 说明

![](https://tva1.sinaimg.cn/large/e6c9d24egy1gzhjrfztmej21hp0mk43g.jpg)



### 方法的妙用

```java

package 面向对象_basic;

public class Method02 {
    public static void main (String[] args) {
        //请遍历一个数组，输出数组的各个元素值
        int[][] map = {{0, 0, 1}, {1, 1, 1}, {1, 1, 3}};

        //使用方法完成输出, 创建MyTools对象
        Mytools tool = new Mytools();
        //使用方法
        tool.printArr(map);
        tool.printArr(map);
        tool.printArr(map);

    }
}

// 把输出的功能，写到一个类的方法中，然后调用该方法即可
class Mytools {
    //方法, 接收一个二维数组
    public void printArr (int[][] map) {
        //对传入的map数组进行遍历输出
        System.out.println("=====");
        for(int i = 0; i < map.length; i++) {
            for(int j = 0; j < map[i].length; j++) {
                System.out.print(map[i][j] + "_");
            }
            System.out.println();
        }
    }

}

```



### 成员方法的定义

```

public 返回数据类型 方法名（形参列表..）{//方法体
	语句;
	return 返回值;
}

```

- public 为一种访问修饰符
- 形参列表：表示成员方法输入cal(int n), getSum(int num1, int num2)
- 返回数据类型：表示成员方法输出，void表示没有返回值
- 方法主体：表示为了实现某一功能代码块
- return语句不是必须的 - 有具体的返回数据类型，就需要写return / 如果结果直接在方法里输出则不需要return



### 方法使用细节

1.修饰符

- 访问修饰符（作用是控制 方法使用的范围），如果不写默认访问，[有四种：public protected 默认 private]，具体后说

2.返回数据类型

- 一个方法最多有一个返回值
- 返回类型可以为任意类型，包括基本类型或引用类型（数组，对象）
- 如果方法要求有返回数据类型，则方法体中最后的执行语句必须为return值；而且要求返回值类型必须和return的值类型一致或兼容
- 如果方法是void，则方法体中可以没有return语句，或者 只写 return

3.方法名

- 最好见名知义，表达出该功能的意思即可，比如 得到两个数的和getSum，开发中按照规范

```java

package 面向对象_basic;

public class MethodDetail {
    public static void main (String[] args) {
        AA a = new AA();
        int[] res = a.getSumAndSub(1, 4);
        System.out.println("和=" + res[0]);
        System.out.println("差=" + res[1]);

    }
}


class AA {
    //1 - 一个方法最多有一个返回值 [思考，如何返回多个结果 返回数组]
    public int[] getSumAndSub(int n1, int n2) {
        int[] res = new int[2];//创建一个数组
        res[0] = n1 + n2;
        res[1] = n1 - n2;
        return res;
    }

    //2 - 返回类型可以为任意类型，包括基本类型或引用类型（数组，对象）- 同上

    //3 - 如果方法要求有返回数据类型，则方法体中最后的执行语句必须为return值；
    // 而且要求返回值类型必须和return的值类型一致或兼容
    public double f1() {
        double d1 = 1.1 * 3;
        int n = 100;
        return n; //int -> double 自动类型转换
    }
    //4 - 如果方法是void，则方法体中可以没有return语句，或者 只写 return
    public void f2() {
        
    }
}

```

4.形参列表

- 一个方法可以有0个参数，也可以有多个参数，中间用逗号隔开，比如getSum(int n1, int n2)
- 参数类型可以为任意类型，包含基本类型或引用类型，比如printArr(int[] [] map)

- 调用带参数的方法时，一定对应着参数列表传入相同类型或兼容类型的参数！【getSum】
- 方法定义时的参数称为形式参数，简称形参；方法调用传入时的参数称为实际参数，简称实参，实参和形参的类型要一致或兼容、个数、顺序必须一致！[演示]

5.方法体 

- 里面写完成功能的具体的语句，可以为输入、输出、变量、运算、分支、循环、方法调用，但里面不能再定义方法，即方法不能嵌套定义

6.方法调用细节说明

- 同一个类中的方法调用：直接调用即可 比如print(参数)；案例演示: A类 sayOk 调用 print()

```java

package 面向对象_basic;

public class Method02 {
    public static void main (String[] args) {
        A a = new A();
        a.sayOK();

    }
}

class A {
    //同一个类中的方法调用：直接调用即可
     public void print(int n) {
         System.out.println("print()方法被调用 n=" + n);
        }
     public void sayOK() { //sayOK调用 print(直接调用)
         print(10);
         System.out.println("继续执行sayOK()");
     }
    }

```

- 跨类中的方法A类调用B类方法：需要通过对象名调用。比如 对象名.方法名(参数)；案例演示：B类 sayHello 调用 print()

```java

package 面向对象_basic;

public class Method {
    public static void main (String[] args) {
        A a = new A();
        a.sayOK();
        a.m1();

    }
}

class A {
    //同一个类中的方法调用：直接调用即可
     public void print(int n) {
         System.out.println("print()方法被调用 n=" + n); // 第一句话
        }
     public void sayOK() { //sayOK调用 print(直接调用)
         print(10);
         System.out.println("继续执行sayOK()"); //第二句话
     }

    //跨类中的方法A调用B类方法：需要通过对象名调用
    public void m1() {
        //创建B对象,然后再调用方法即可
        System.out.println("m1方法被调用"); //第三句话
        B b = new B();
        b.hi();
        System.out.println("m1()继续执行"); //第五句话


    }
}

class B {
    public void hi() {
        System.out.println("B类中的 hi()被执行"); //第四句话
    }
}

```

- 特别说明：跨类的方法调用和方法的修饰符相关（先暂时提及）



### 方法练习题1

1.编写类AA，有一个方法：判断一个数是奇数odd还是偶数，返回boolean

```java

package 面向对象_basic;

public class Exercise01 {
    public static void main (String[] args) {
        AA a = new AA();
        if(a.isOdd(2)) { //这样的写法以后会看到很多
            System.out.println("是奇数");
        } else {
            System.out.println("是偶数");
        }
    }
}

//编写类AA，有一个方法：判断一个数是奇数odd还是偶数，返回boolean
class AA {
    //思路
    //1 - 方法的返回类型 boolean
    //2 - 方法的名字 isOdd
    //3 - 方法的形参 (int num)
    //4 - 方法体 , 判断
    public boolean isOdd(int num) {
        return num % 2 !=0;
    }
}

```

2.根据行、列、字符打印 对应行数和列数的字符，比如：行：4，列：4，字符#，则根据打印相应的效果

```java

package 面向对象_basic;

public class Exercise02 {
    public static void main (String[] args) {
        AA a = new AA();
        //使用print方法
        a.print(4,4);
        }
    }
    
class AA {
    
    // 根据行、列、字符打印 对应行数和列数的字符，
    // 比如：行：4，列：4，字符#，则根据打印相应的效果
    /*
        ####
        ####
        ####
        ####
     */

    //思路
    //1 - 方法的返回类型 void
    //2 - 方法的名字 print
    //3 - 方法的行参 (int row, int column)
    //4 - 方法体，循环
    public void print(int row, int column){
        for(int i = 0; i < row; i++) {
            for(int j = 0; j < column; j++) { //输出每一行
                System.out.print("#");
            }
            System.out.println(); //换行
        }
    }
}

```





## 成员方法传参机制

方法的传参机制对我们今后的编程非常重要，一定要搞的清清楚楚明明白白



### 基本数据类型的传参机制

```java

package 面向对象_basic;

public class MethodParameter01 {
    public static void main (String[] args) {
        int a = 10;
        int b = 20;
        //创建AA对象
        AA obj = new AA();
        obj.swap(a, b); //调用swap方法
        System.out.println("main 主方法 a=" + a + " b=" + b); // a = 10 b = 20


        }
    }

class AA {
    public void swap (int a, int b) {
        System.out.println("\na和b交换前的值\na=" + a + "\tb=" + b); //a = 10 b=20
        //完成来 a 和 b 的交换
        int tmp = a;
        a = b;
        b = tmp;
        System.out.println("\na和b交换后的值\na=" + a + "\tb=" + b);//a = 20 b = 10
    }


}

// 两个栈是独立的数据空间，基本的数据类型不是引用，变化不会影响到彼此

```

结论及示意图：基本数据类型，传递的是值（值拷贝），形参的任何改变不影响实参

![](https://tva1.sinaimg.cn/large/e6c9d24egy1gzilrx6vvoj20uq0rd42n.jpg)



### 引用数据类型的传参机制

```java

package 面向对象_basic;

public class MethodParameter02 {
    public static void main (String[] args) {
        //测试
        B b = new B();
        int[] arr = {1, 2, 3};
        b.test100(arr);//调用方法
        System.out.println("main的arr数组");
        //遍历数组
        for(int i = 0; i < arr.length; i++) {
            System.out.print(arr[i] + "\t");
        }
        System.out.println();
        }
    }

class B {
    //B类中编写一个方法test100
    //可以接收一个数组，在方法中修改该数组，看看原来的数组是否变化
    public void test100(int[] arr) {
        arr[0] = 200;
        //遍历数组
        System.out.println("test100的arr数组");
        for(int i = 0; i < arr.length; i++) {
            System.out.print(arr[i] + "\t");
        }
        System.out.println();
    }
}

```

结论及示意图：引用类型传递的是地址（传递也是值，但是值是地址），可以通过形参影响实参

![](https://tva1.sinaimg.cn/large/e6c9d24egy1gzimi6qmuxj20u30nvq6h.jpg)

修改一：

```java

package 面向对象_basic;

public class MethodParameter02 {
    public static void main (String[] args) {
        B b = new B();
        //测试
        Person p = new Person();
        p.name = "jack";
        p.age = 10;

        b.test200(p);
        System.out.println("main的p.age=" + p.age);
        }
    }

class Person {
    String name;
    int age;
}


class B {
    public void test200(Person p) {//形参为Person p - 复制其地址
        p.age = 10000;//修改对象属性

    }
}
//这里test200()的形参是一个Person类的对象，main里面定义了一个Person类的对象p，然后把这个对象再传到test200方法里，那么自然这个方法里的p.age改变的就是p对象的属性

```

![](https://tva1.sinaimg.cn/large/e6c9d24egy1gzin2m6imvj20uo0t7q6o.jpg)

修改二：

```java

package 面向对象_basic;

public class MethodParameter02 {
    public static void main (String[] args) {
        B b = new B();
        //测试
        Person p = new Person();
        p.name = "jack";
        p.age = 10;

        b.test200(p);
        //测试题，如果 test200 执行的是 p = null 下面的结果是 10
        System.out.println("main的p.age=" + p.age);
        }
    }

class Person {
    String name;
    int age;
}


class B {
    public void test200(Person p) { //形参Person p 复制其地址
        //p.age = 10000; 修改对象属性
        //思考
        p = null;

    }
}

//输出为10

```

![](https://tva1.sinaimg.cn/large/e6c9d24egy1gzinr0p02rj20pd0gtdhb.jpg)

修改三：

```java

package 面向对象_basic;

public class MethodParameter02 {
    public static void main (String[] args) {
        B b = new B();
        //测试 如果 test200 执行的是 p=new Person()...，下面输出的是？ 
        Person p = new Person();
        p.name = "jack";
        p.age = 10;

        b.test200(p);
        //测试题，如果 test200 执行的是 p = null 下面的结果是 10
        System.out.println("main的p.age=" + p.age);
        }
    }

class Person {
    String name;
    int age;
}


class B {
    public void test200(Person p) { //形参Person p 复制其地址
        //p.age = 10000; 修改对象属性
        //思考
        p = new Person();
        p.name = "tom";
        p.age = 99;

    }
}

//输出还是10

```

![](https://tva1.sinaimg.cn/large/e6c9d24egy1gzio50cnrqj20vw0m0wi6.jpg)



### 练习题

```java

package 面向对象_basic;

public class Exercise01 {
    public static void main (String[] args) {
        int[][] map = {{0,0,1},{1,1,1},{1,1,3}};
        MyTools a = new MyTools();
        a.printArr(map);

    }
}

class MyTools {
    public void printArr(int[][] map) {
        System.out.println("=====");
        for(int i = 0; i < map.length; i++) {
            for (int j = 0; j < map[i].length; j++) {
                System.out.print(map[i][j] + "");
            }
            System.out.println();
        }
    }
}

```

```java

package 面向对象_basic;

public class Exercise02 {
    public static void main (String[] args) {
        Person p = new Person();
        p.name = "harry";
        p.age = 100;
        //创建tools
        MyTools tools = new MyTools();
        tools.copyPerson(p);
        Person p2 = tools.copyPerson(p);

        //到此 p 和 p2 是 Person对象，但是是两个独立的对象，属性相同
        System.out.println("p的属性 age=" + p.age + "名字 = " + p.name);
        System.out.println("p2的属性 age=" + p2.age + "名字 = " + p2.name);
        //提示：可以通过 对象比较看是否为同一个对象, 强调对象
        System.out.println(p!=p2);

    }
}

class Person {
    String name;
    int age;
}

class MyTools {
    //编写一个方法copyPerson，可以复制一个Person对象，返回复制的对象 克隆对象
    //注意要求得到新对象和原来的对象是两个独立的对象，只是他们的属性相同
    //
    //编写方法的思路
    //思路
    //1 - 方法的返回类型 Person
    //2 - 方法的名字 copyPerson
    //3 - 方法的形参 (Person P)
    //4 - 方法体，完成一个复制
    public Person copyPerson(Person p) {
        //创建一个新的对象
        Person p2 = new Person();
        p2.name = p.name; //把原来对象的名字赋给p2.name
        p2.age = p.age; //把原来对象的年龄赋给p.name
        return p2;
    }
}

```

![](https://tva1.sinaimg.cn/large/e6c9d24egy1gzipg40a9wj20w00mgtby.jpg)





## 方法递归调用

简单的说：递归就是方法自己调用自己，每次调用时传入不同的变量，递归有助于编程者解决复杂问题，同时可以让代码变得简洁


### 递归能解决什么问题？

1.各种数学问题：8皇后问题，汉诺塔，阶乘问题，迷宫问题，球和篮子的问题（Google编程大赛）

2.各种算法中也会使用到递归，比如快排，归并排序，二分查找，分治算法等

3.将用栈解决的问题 --> 递归代码比较简洁


### 递归执行机制

```java

//打印问题
package 面向对象_basic;

public class Recursion01 {
    public static void main (String[] args) {
        T t1 = new T();
        t1.test(4);//输出什么

    }
}

class T {
    //分析
    public void test (int n) {
        if(n > 2) {
            test(n - 1);
        }
        System.out.println("n=" + n);
    }
}

```

![](https://tva1.sinaimg.cn/large/e6c9d24egy1gziw2esf19j21bo0kyq7o.jpg)

```java

//阶乘练习
package 面向对象_basic;

public class Method02 {
    public static void main (String[] args) {
        T t1 = new T();
        int res = t1.factorial(5);
        System.out.println("res=" + res);



    }
}

class T {
    //factorial 阶乘
    public int factorial (int n) {
        if (n == 1) {
            return 1;
        } else {
            return factorial(n - 1) * n;
        }
    }
}
```

![](https://tva1.sinaimg.cn/large/e6c9d24egy1gziwkdck3cj20fo0modhp.jpg)



### 递归重要规则

1.执行一个方法时，就创建一个新的受保护的独立空间（栈空间）

2.方法的局部变量是独立的，不会相互影响，比如n变量

3.如果方法中使用的是引用类型变量（比如数组，对象），就会共享该引用类型的数据

4.递归必须向退出递归的条件逼近，否则就是无限递归，出现StackOverFlowError

5.当一个方法执行完毕，或者遇到return，就会返回，遵守谁调用，就将结果返回给谁，同时当方法执行完毕或返回时，该方法也就执行完毕



### 课堂练习

1.使用递归的方式求出斐波那契数1,1,2,3,5,8,13....给你一个整数n, 求出它的值是多少

```java

package 面向对象_basic;

public class fibonacci {
    public static void main (String[] args) {
        T t1 = new T();
        int n = 0;
        int res = t1.fibonacci(n);
        if(res != -1){
            System.out.println("当n="+ n +"对应的斐波拉契数=" + res);
        }

    }
}

class T {
    /*
    使用递归的方式求出斐波那契数1,1,2,3,5,8,13....给你一个整数n, 求出它的值是多少
    思路分析
    1 - 当n = 1 斐波那契数 是1
    2 - 当n = 2 斐波那契数 是1
    3 - 当n > 3 斐波那契数 是前两个数的和
    4 - 这里就是一个递归的思路
     */
    public int fibonacci(int n) {
        if(n >= 1) {
            if(n == 1 || n == 2) {
                return 1;
            } else {
                return fibonacci(n-1) + fibonacci(n-2);
            }
        }else {
            System.out.println("要求输入n为大于1的整数");
            return -1;
        }
    }
}

```



2.猴子吃桃子问题：有一堆桃子，猴子第一天吃了其中的一半，并再多吃了一个，以后每天猴子都吃其中的一半，然后再多吃一个。当到第10天时，想再吃时 (即还没吃)，发现只有一个桃子了。问题：最初共多少个桃子？

```java

package 面向对象_basic;

public class monkey {
    public static void main (String[] args) {
        T t1 = new T();
        //桃子问题
        int day = 0;
        int peachNum = t1.peach(day);
        if(peachNum != -1) {
            System.out.println("第" + day + "天有" + peachNum + "个桃子");
        }

}
}

class T {
    /*
    猴子吃桃子问题：有一堆桃子，猴子第一天吃了其中的一半，并再多吃了一个，
    以后每天猴子都吃其中的一半，然后再多吃一个。
    当到第10天时，想再吃时 (即还没吃)，发现只有一个桃子了。问题：最初共多少个桃子？

    思路分析 逆推
    1 - day = 10时 有 1个桃子
    2 - day = 9时 有 (day10 + 1) * 2 = 4
    3 - day = 8时 有 (day9 + 1) * 2 =  10
    4 - 规律就是 前一天的桃子 = （后一天桃子 + 1）* 2
    5 - 递归
     */
    public int peach(int day) {
        if(day == 10) {//第10天，只有1个桃子
            return 1;
        } else if (day >= 1 && day <= 9) {
            return (peach(day + 1) + 1) * 2;
        } else {
            System.out.println("day在1-10");
            return -1;
        }
    }
}

```



### 迷宫问题

1.小球得到的路径，和程序员设置的找路策略有关即：找路的上下左右的顺序相关

2.再得到小球路径时，可以先使用（下右上左），再改成（上右下左），看看路径是不是有变化

3.测试回溯现象

4.扩展思考：如何求出最短路径

```java

package 面向对象_basic;

public class maze {
    public static void main (String[] args) {
        //思路
        // 1 - 先创建迷宫，用二维数组表示 int[][] map = new int[8][7]
        // 2 - 先规定 map 数组的元素值：0 表示可以走 1 表示障碍物
        int[][] map = new int[8][7];
        // 3 - 将最上面的一行和最下面的一行，全部设置为 1
        for(int i = 0; i < 7; i++) {
            map[0][i]=1;
            map[7][i]=1;
        }
        // 4 - 将最右边一列和最左面一列，全部设为1
        for(int i = 0; i < 8; i++){
            map[i][0] = 1;
            map[i][6] = 1;
        }

        map[3][1] = 1;
        map[3][2] = 1;


        //输出当前的地图
        System.out.println("=====当前地图情况====");
        for(int i = 0; i < map.length; i++) {
            for(int j = 0; j < map[i].length; j++) {
                System.out.print(map[i][j] + " ");//输出一行
            }
            System.out.println();
        }
        //使用findWay给老鼠找路
        T t1 = new T();
        t1.findWay(map,1,1);

        System.out.println("\n=====找路的情况如下=====");
        for(int i = 0; i < map.length; i++) {
            for(int j = 0; j < map[i].length; j++) {
                System.out.print(map[i][j] + " ");//输出一行
            }
            System.out.println();
        }


}
}

class T {
    // 使用递归回溯的思想来解决老鼠出迷宫 （i-行 j-列）
    // 1 - findWay方法就是专门来找出迷宫的路径
    // 2 - 如果找到，就返回 true，否则返回false
    // 3 - map 就是二维数组，即表示迷宫
    // 4 - i，j 就是老鼠的位置 初始化位置为(1,1)
    // 5 - 因为我们是递归的找路，所以先规定 map数组的各个值的含义
    //     0 表示可以走 1 表示障碍物；2 表示可以走通；3 表示走过，但是走不通是死路
    // 6 - 当map[6][5] = 2时，就说明找到通路可以结束，否则就继续找
    // 7 - 先确定老鼠找路策略 下->右->上->左
    public boolean findWay(int[][] map, int i, int j){
        if(map[6][5] == 2){//说明已经找到
            return true;
        } else {
            if(map[i][j] == 0) { //说明可以走
                //假定可以走通
                map[i][j] = 2;
                //使用找路策略，来确定该位置是否真的可以走通
                //下->右->上->左
                if(findWay(map, i + 1, j)) { //先走下
                    return true;
                } else if(findWay(map, i, j+1)) {//右
                    return true;
                } else if(findWay(map, i-1, j)) { //上
                    return true;
                } else if(findWay(map, i, j-1)) { //左
                    return true;
                } else {
                    map[i][j] = 3;
                    return false;
                }
            } else { //map[i][j] = 1,2,3
                return false;
            }
        }
    }
}

```



### 汉诺塔问题

```java

package 面向对象_basic;

public class HanoiTower {
    public static void main (String[] args) {
        //思路
        Tower tower = new Tower();
        tower.move(7,'A','B','C');
}
}

class Tower {
    //方法
    //num 表示要移动的个数 a, b, c 分别表示A塔，B塔，C塔
    public void move(int num, char a, char b, char c) {
        //如果只有一个盘 num=1
        if(num == 1) {
            System.out.println(a + "->" + c);
        } else {
            //如果有多个盘，可以看成两个，最下面和上面的所有盘
            // 1-先移动上边所有的盘到b，借助 c
            move(num-1, a, c, b);
            // 2-把最下面的盘，移动到c
            System.out.println(a + "->" + c);
            // 3-再把b塔所有盘，移动到c，借助a塔
            move(num-1, b, a, c);

        }
    }
}

```



### 八皇后问题

思路分析

1.第一个皇后先放在第一行第一列

2.第二个皇后放在第二行第一列，然后判断是否OK，如果不OK，继续放在第二列、第三列、依次把所有列都放完，找到一个合适的

3.继续第三个皇后，还是第一列、第二列....直到第8个皇后也能放在一个不冲突的位置，算是找到一个正确解

4.当得到第一个正确解时，在栈回退到上一个栈时，就会开始回溯，即将第一个皇后，放到第一列的正确解，全部得到

5.然后回头继续第一个皇后放第二列，后面继续循环执行1，2，3，4的步骤



## 方法重载 OverLoad

### 重载介绍

1.基本介绍：java中允许同一个类中，多个同名方法的存在，但要求形参列表不一致。比如：System.out.println(); out是PrintStream类型

2.重载的好处

- 减轻了起名的麻烦
- 减轻了记名的麻烦


### 方法重载快速入门

```java

package 面向对象_basic;

public class OverLoad {
    public static void main (String[] args) {
        MyCalculate mc = new MyCalculate();
        System.out.println(mc.calculate(1,2));
        System.out.println(mc.calculate(1.1,2));
}
}

class MyCalculate {
    //两个整数的和
   public int calculate(int n1, int n2) { //被第一个调用
       return n1 + n2;
   }
   //一个整数，一个double的和
    public double calculate(int n1, double n2){
       return n1 + n2;
    }
   //一个double 一个int和
   public double calculate(double n1, int n2) { //被第二个调用
       return n1 + n2;
   }
   //三个int的和
   public int calculate(int n1, int n2, int n3) {
       return n1 + n2 + n3;
   }

}

```



### 方法重载细节

1.方法名：必须相同

2.形参列表：必须不同（形参类型或个数或顺序，至少有一样不同，参数名无要求）

```java

public int calculate(int n1, int n2) { //被第一个调用
       return n1 + n2;
   }

public int calculate(int a1, int a2) { //没有构成重载，而是方法的重复定义
  return a1 + a2;
	}

```

3.返回类型：无要求

```java

public int calculate(int n1, int n2) { //被第一个调用
       return n1 + n2;
   }

public void calculate(int n1, int n2) { //没有构成方法重载, 还是方法的重复定义
  int res = n1 + n2;
   }

```



### 重载课堂练习

1.第一题判断题

![]https://tva1.sinaimg.cn/large/e6c9d24egy1gzjzarpra3j210m0fh42e.jpg)

2.第二题：编写程序，类Method中定义三个重载方法并调用。方法名为m。三个方法分别接受接收一个int参数、一个字符串参数。分别执行平方运算并输出结果，相乘并输出结果，输出字符串信息。在主类的main()方法中分别用参数区别调用三个方法

```java

package 面向对象_basic;

public class Overload {
    public static void main (String[] args) {
        // 在主类的main()方法中分别用参数区别调用三个方法
        Methods method = new Methods();
        method.m(10); //输出100
        method.m(10,20); //输出200
        method.m("你好"); //输出 你好

}
}

/*
编写程序，类Method中定义三个重载方法并调用。方法名为m。
三个方法分别接受接收一个int参数、一个字符串参数。
分别执行平方运算并输出结果，相乘并输出结果，输出字符串信息。
在主类的main()方法中分别用参数区别调用三个方法
 */

class Methods {
    //分析
    //1 - 方法名 m
    //2 - 形参(int)
    //3 - void
    public void m(int n) {
        System.out.println("平方=" + (n * n));
    }

    //分析
    //1 - 方法名 m
    //2 - 形参(int, int)
    //3 - void
    public void m(int n1, int n2) {
        System.out.println("平方=" + (n1 * n2));
    }

    //分析
    //1 - 方法名 m
    //2 - 形参(String)
    //3 - void
    public void m(String str) {
        System.out.println("传入的Str=" + str);
    }

}

```

3.在Methods类，定义三个重载方法max()，第一个方法，返回两个int值中的最大值，第二个方法，返回两个double值中的最大值，第三个方法，返回三个double值中的最大值，并分别调用三个方法

```java

package 面向对象_basic;

public class Method02 {
    public static void main (String[] args) {
        Methods method = new Methods();
        System.out.println(method.max(10,24));
        System.out.println(method.max(11.2,22.4));
        System.out.println(method.max(11.2,22.4,33));
    }
}

/*
在Methods类，定义三个重载方法max()，
第一个方法，返回两个int值中的最大值，
第二个方法，返回两个double值中的最大值，
第三个方法，返回三个double值中的最大值，并分别调用三个方法
 */

class Methods {
    //分析
    //1 - 方法名 max
    //2 - 形参(int, int)
    //3 - int
    public int max(int n1, int n2) {
        return n1 > n2 ? n1 : n2;
    }

    //分析
    //1 - 方法名 max
    //2 - 形参(double, double)
    //3 - double
    public double max (double a1, double a2) {
        return a1 > a2 ? a1 : a2;
    }

    //分析
    //1 - 方法名 max
    //2 - 形参(double, double, double)
    //3 - double
    public double max (double a1, double a2, double a3) {
        //求出 a1 和 a2 的最大值
        double max1 = a1 > a2 ? a1 : a2;
        return max1 > a3 ? max1 : a3;
    }
}

}

```



## 可变参数

### 可变参数使用

1.基本概念

java允许将同一个类中多个同名同功能但参数个数不同的方法，封装成一个方法

2.基本语法

```java

访问修饰符 返回类型 方法名 (数据类型...形参名) { 
}
  
```

3.快速入门案例

```java

package 面向对象_basic;

public class VarParameter {
    public static void main (String[] args) {
        HspMethod m = new HspMethod();
        System.out.println(m.sum(1,5,100)); //106
        System.out.println(m.sum(1,9));//10
    }
}



class HspMethod {
        //可以计算 2个数的和，3个数的和....
        //可以使用方法重载

    //....
    //上面的三个方法名称相同，功能相同，参数个数不同 -> 使用可变参数
    //解读
    //1 - int... 表示接收的是可变参数，类型是int，即可以接收多个int(0-多)
    //2 - 使用可变参数时，可以当做数组来使用 即 nums 可以当作数组
    //3 - 遍历求和即可
    public int sum(int... nums){
        System.out.println("接收的参数个数=" + nums.length);
        int res = 0;
        for(int i = 0; i < nums.length; i++) {
            res += nums[i];
        }
       return res;
    }

}

```



### 注意事项和使用细节

1.可变参数的实参可以为0个或任意多个

2.可变参数的实参可以为数组

```java

package 面向对象_basic;

public class VarParameter {
    public static void main (String[] args) {
        //细节：可变参数的实参可以为数组
        int[] arr = {1,2,3};
        T t1 = new T();
        t1.f1(arr);

    }
}

class T {

    public void f1(int... nums){
        System.out.println("长度=" + nums.length);

    }
}

```

3.可变参数的本质就是数组

4.可变参数可以和普通类型的参数一起放在形参列表，但必须保证可变参数在最后

```java

   public void f2(String str, double... nums) {
        
    }

```

5.一个形参列表中只能出现一个可变参数



### 可变参数练习

有三个方法，分别实现返回姓名和两门课成绩（总分），返回姓名和三门课成绩（总分），返回姓名和五门课成绩（总分）。封装成一个可变参数的方法

类名HspMethod 方法名showScore

```java

package 面向对象_basic;

public class VarParameter {
    public static void main (String[] args) {
        HspMethod hm = new HspMethod();
        //方法的调用，return返回的值也就返回到方法的调用中
        System.out.println(hm.showScore("harry", 90.1,80.0,78.9));


    }
}

class HspMethod {
    /*
    有三个方法，分别实现返回姓名和两门课成绩（总分），
    返回姓名和三门课成绩（总分），
    返回姓名和五门课成绩（总分）。封装成一个可变参数的方法
     */

    //分析 1-方法名 showScore 2-形参(String，double...) 3-返回String
    public String showScore(String name, double...scores){
        double totalScore = 0;
        for(int i = 0; i < scores.length; i++) {
            totalScore += scores[i];
        }
        return name + "有" + scores.length + "门课的成绩总分为=" + totalScore;
    }
}

```



## 作用域

### 作用域基本使用

面向对象中，变量作用域是非常重要的知识点，相对来说不是特别好理解，请认真听与思考，要求深刻掌握变量作用域

1.在java编程中，主要的变量就是属性（成员变量）和局部变量

2.我们说的局部变量一般是指在成员方法中定义的变量

```java

class Cat {
  //全局变量：也就是属性，作用域为整个类体 Cat类：cry eat 等方法使用属性
  //属性在定义时，可以直接赋值
  int age = 10; //指定值是10
    public void cry() {
        //1.局部变量一般是指在成员方法中定义的变量
        //2.n和name就是局部变量
      	//3.n和name的作用域在cry方法中
        int n = 10;
        String name = "jack";
    }


```

3.Java中作用域的分类

局部变量：也就是除了属性之外的其他变量，作用域为定义它的代码块中

```java

class Cat {
    public void cry() {
        //1.局部变量一般是指在成员方法中定义的变量
        //2.n和name就是局部变量
        //3.n和name的作用域在 cry方法中
        int n = 10;
        String name = "jack";
    }
}

```

全局变量：也就是属性，作用域为整个类体 Cat类：cry eat 等方法使用属性

```java

class Cat {
    //全局变量：也就是属性，作用域为整个类体 Cat类：cry eat 等方法使用属性
    //属性在定义时，可以直接赋值
    int age = 10; //
    
    public void cry() {
        //1.局部变量一般是指在成员方法中定义的变量
        //2.n和name就是局部变量
        //3.n和name的作用域在 cry方法中
        int n = 10;
        String name = "jack";
        System.out.println("在cry中使用属性age=" + age );
    }
    public void eat() {
        System.out.println("在eat方法中使用属性age=" + age );

        System.out.println("在eat方法中使用 cry的变量 name=" + name );//错误 
    }
}

```

4.全局变量可以不赋值，直接使用，因为有默认值，局部变量必须赋值后，才能使用，因为没有默认值

```java

class Cat {
    //全局变量：也就是属性，作用域为整个类体 Cat类：cry eat 等方法使用属性
    //属性在定义时，可以直接赋值
    int age = 10; //

    //全局变量可以不赋值，直接使用，因为有默认值，
    double weight; //默认值是0.0
    // 局部变量必须赋值后，才能使用，因为没有默认值
    public void hi() {
        int num;
        System.out.println("num=" + num);//报错
    }
}

```



### 作用域的注意事项和使用细节

1.属性和局部变量可以重名，访问时遵循就近原则

```java

package 面向对象_basic;

public class VarScopeDetail {
    public static void main (String[] args) {
        Person p1 = new Person();
        p1.say();

    }
}

class Person {
   String name = "jack";
   public void say() {
       //属性和局部变量可以重名，访问时遵守就近原则
       String name = "king";
       System.out.println("say() name=" + name);//输出king
   }
}

```

2.在同一个作用域中，比如在同一个成员方法中，两个局部变量，不能重名

```java

public void hi() {
  String address = "北京";
  String address = "上海"; 
  //错误，重复定义变量，会报错
}

```

3.属性生命周期长，伴随着对象的创建而创建，伴随着对象的销毁而销毁。局部变量，生命周期较短，伴随着它的代码块的执行而创建，伴随着代码块的结束而死亡，即在一次方法调用过程中

```java

package 面向对象_basic;

public class VarScopeDetail {
    public static void main (String[] args) {
        Person p1 = new Person();
        /*
        属性生命周期长，伴随着对象的创建而创建，伴随着对象的销毁而销毁。
        局部变量，生命周期较短，伴随着它的代码块的执行而创建，
        伴随着代码块的结束而死亡，即在一次方法调用过程中
         */
        p1.say();//当执行say方法时，say方法的局部变量比如name, 会创建，当say执行完毕后
        //name局部变量就销毁，但是属性（全局变量）仍然可以使用

    }
}

class Person {
   String name = "jack";
   public void say() {
       //属性和局部变量可以重名，访问时遵守就近原则
       String name = "king";
       System.out.println("say() name=" + name);//输出king
   }
}

```

4.作用域范围不同

全局变量/属性：可以被本类使用，或其他类使用（通过对象调用）

局部变量：只能在本类对应的方法中使用

```java

package 面向对象_basic;

public class VarScopeDetail {
    public static void main (String[] args) {
        Person p1 = new Person();
        /*
        属性生命周期长，伴随着对象的创建而创建，伴随着对象的销毁而销毁。
        局部变量，生命周期较短，伴随着它的代码块的执行而创建，
        伴随着代码块的结束而死亡，即在一次方法调用过程中
         */
        p1.say();//当执行say方法时，say方法的局部变量比如name, 会创建，当say执行完毕后
        //name局部变量就销毁，但是属性（全局变量）仍然可以使用
        T t1 = new T();
        t1.test();//第一种跨类访问对象属性的方式

        t1.test2(p1);//第二种跨类访问对象属性的方式

    }
}

class T {
    public void test() {
        Person p1 = new Person();
        System.out.println(p1.name); //创建新的来访问jack
    }

    public void test2(Person p) {
        System.out.println(p.name); //jack - 别的作用域的person传入
    }
}

class Person {
   String name = "jack";
   public void say() {
       //属性和局部变量可以重名，访问时遵守就近原则
       String name = "king";
       System.out.println("say() name=" + name);//输出king
   }
}

```

5.修饰符不同

全局变量/属性可以加修饰符

局部变量不可以加修饰符



## 构造方法/构造器

### 构造器基本介绍

1.基本语法

```java

[修饰符] 方法名(形参列表) {
  方法体; 
}

```

-  构造器的修饰符可以默认 public protected private
-  构造器没有返回值
-  method名 和class名字必须一样
-  参数列表 和 成员方法一样的规则
-  构造器的调用系统完成

2.基本介绍

构造方法又叫构造器constructor，是class的一种特殊的方法，它的主要作用是完成<u>新对象的初始化</u>，它有几个特点:

- 方法名和类名相同
- 没有返回值
- 在创建对象时，系统会自动的调用该类的构造器完成对对象的初始化

#### 快速入门

```java

package 面向对象_basic;

public class Constructor {
    public static void main (String[] args) {
        //当我们new一个对象时，直接通过构造器指定名字和年龄
        Person p1 = new Person("smith", 80);
        System.out.println("p1的信息如下");
        System.out.println("p1对象name=" + p1.name); //smith
        System.out.println("p1对象age=" + p1.age); //80

    }
}

//在创建人类的对象时，直接指定这个对象的年龄和姓名
class Person {
    String name;
    int age;
    //构造器
    //解读
    //1 - 构造器没有返回值，也不能写void
    //2- 构造器的名称和类名Person一样
    //3- (String pName, int pAge)是构造器形参列表，规则和成员方法一样
    public Person(String pName, int pAge) {
        System.out.println("构造器被调用，完成对象属性的初始化");
        name = pName;
        age = pAge;
    }
}

```

### 注意事项和使用细节

1.一个类可以定义多个不同的构造器，即构造器重载 - 比如：我们可以再给Person类定义一个构造器，用来创建对象的时候，只指定人名，不需要指定年龄

```java

package 面向对象_basic;

public class Constructor {
    public static void main (String[] args) {
        //当我们new一个对象时，直接通过构造器指定名字和年龄
        Person p1 = new Person("harry", 40);//调用第一个构造器
        Person p2 = new Person("tom");//调用第二个构造器

    }
}

//在创建人类的对象时，直接指定这个对象的年龄和姓名
class Person {
    String name;
    int age;//默认0
    //第一个构造器
    public Person(String pName, int pAge) {
        System.out.println("构造器被调用，完成对象属性的初始化");
        name = pName;
        age = pAge;
    }
    //第二个构造器，只指定人名，不需要指定年龄
    public Person(String pName) {
        System.out.println("构造器被调用，完成对象属性的初始化");
        name = pName;
    }
}

```

2.构造器名和类名相同

3.构造器没有返回值

4.构造器是完成对象的初始化，并不是创建对象

5.在创建对象时，系统自动的调用该类的构造方法

### 构造器使用细节

1.如果没有定义构造器，系统会自动给类生成一个默认无参构造方法（也叫默认构造法），比如Dog (){}, 使用javap指令 反编译看看 <javap的使用>

```java

public class Constructor {
    public static void main (String[] args) {
        //当我们new一个对象时，直接通过构造器指定名字和年龄
        Person p1 = new Person("harry", 40);//调用第一个构造器
        Person p2 = new Person("tom");//调用第二个构造器
        Dog dog1 = new Dog();

    }
}

class Dog {
    //如果没有定义构造器，系统会自动给类生成一个默认无参构造方法（也叫默认构造法）
    //使用javap指令 反编译看看
    /*
        默认构造器
        Dog() {

        }
     */
}

```

2.一旦定义了自己的构造器，默认的构造器就覆盖了，就不能再使用默认的无参构造器，除非显示的定义一下，即：Dog () {} (这一点很重要)

```java

public class Constructor {
    public static void main (String[] args) {
        
        Dog dog1 = new Dog();//使用的是默认的无参构造器，报错 - 如果还想用必须显示定义一下

    }
}

class Dog {
    //如果没有定义构造器，系统会自动给类生成一个默认无参构造方法（也叫默认构造法）
    //使用javap指令 反编译看看
    /*
        默认构造器
        Dog() {

        }
     */

    //一旦定义了自己的构造器，默认的构造器就覆盖了，就不能再使用默认的无参构造器，
    // 除非显示的定义一下，即：Dog () {} (这一点很重要)
    //
    public Dog(String dName) {
        //...
    }
    
    Dog() {//显示的定义一下 无参构造器
        
    }
}

```

### 构造器课堂练习

在前面定义的Person类中添加两个构造器：

第一个无参构造器：利用构造器设置所有人的age属性初始值都为18

第二个带pName和pAge两个参数的构造器：使得每次创建Person对象的同时初始化对象和age属性值和name属性值。分别使用不同的构造器，创建对象

```java

package 面向对象_basic;

public class Constructor {
    public static void main (String[] args) {
        
        //p1和p2是两个不同的对象
        Person p1 = new Person(); //无参构造器
        
        //下面输出 name = null, age = 18
        System.out.println("p1的信息 name=" + p1.name + " age=" + p1.age);
        
        Person p2 = new Person("scott",50);
        //下面输出 name = scott, age = 50
        System.out.println("p2的信息 name=" + p2.name + " age=" + p2.age);

    }
}

/*
第一个无参构造器：利用构造器设置所有人的age属性初始值都为18
第二个带pName和pAge两个参数的构造器：
使得每次创建Person对象的同时初始化对象和age属性值和name属性值。
分别使用不同的构造器，创建对象
 */


class Person {
    String name; //默认值null
    int age;//默认值0
    // 第一个无参构造器：利用构造器设置所有人的age属性初始值都为18
    public Person() {
        age = 18;//
    }
    //第二个带pName和pAge两个参数的构造器
    public Person(String pName, int pAge) {
        name = pName;
        age = pAge;
    }

}

```



## 对象创建的流程分析

![](https://tva1.sinaimg.cn/large/e6c9d24egy1gzm5b285qtj21do0r7gu4.jpg)

流程分析

1.加载Person类信息(Person.class), 只会加载一次

2.在堆中分配空间(地址)

3.完成对象初始化

 [3.1 默认初始化 age=0 name=null 

3.2 显示初始化 age=90, name=null 

3.3 构造器初始化 age = 20, name=小倩]

4.把对象在堆中的地址，返回给p(p是对象名/对象的引用)

### 类定义的完善

![](https://tva1.sinaimg.cn/large/e6c9d24egy1gzm5le49txj212o0hf40n.jpg)



## this


### this 入门

1.什么是this

java虚拟机会给每个对象分配this，代表当前对象。坦白的讲，要明白this不是件容易的事

```java

package 面向对象_basic;

public class Method02 {
    public static void main (String[] args) {
        Dog dog1 = new Dog("harry", 12);
        dog1.info();
    }
}

class Dog {
    String name;
    int age;
    
    public Dog(String name, int age) {//构造器
        //this.name 就是当前对象的属性name
        this.name = name;
        //this.age 就是当前对象的属性age
        this.age = age;
    }
    
    public void info(){//成员方法调用属性信息
        System.out.println(name + "\t" + age + "\t");
    }
}

```

### this 本质

![](https://tva1.sinaimg.cn/large/e6c9d24egy1gzmcrx9w8oj21l70o80z1.jpg)

```java

package 面向对象_basic;

public class This {
    public static void main (String[] args) {
        Dog dog1 = new Dog("harry", 12);
        System.out.println("dog1的hashcode=" + dog1.hashCode());
        dog1.info();

        Dog dog2 = new Dog("may",10);
        System.out.println("dog2的hashcode=" + dog2.hashCode());
        dog2.info();
    }
}



class Dog {
    String name;
    int age;

    public Dog(String name, int age) {//构造器
        //this.name 就是当前对象的属性name
        this.name = name;
        //this.age 就是当前对象的属性age
        this.age = age;
        System.out.println("this.hashCode=" + this.hashCode());
    }

    public void info(){//成员方法调用属性信息
        System.out.println(name + "\t" + age + "\t");
    }
}

```



### this小结

this小结：哪个对象调用，this就代表哪个对象



### this 使用细节

1.this关键字可以用来访问<u>本类的属性</u>，<u>方法</u>和<u>构造器</u>

```java

public void f3() {
  String name = "smith";
  //传统方式
  System.out.println("name=" + name + "num=" + num);//smith 100
  //也可使用this访问属性
  System.out.println("name=" + this.name + " num" + num)//jack 100
}

```

2.this用来区分当前类的属性和局部变量

3.访问成员方法的语法：this.方法名(参数列表) ;

```java

package 面向对象_basic;

public class This {
    public static void main (String[] args) {
        T t1 = new T();
        t1.f2();

    }
}



class T {
    //细节：访问成员方法的语法：this.方法名(参数列表)
    public void f1() {
        System.out.println("f1() 方法...");
    }

    public void f2() {
        System.out.println("f2 方法...");
        //调用本类的f1
        //第一方式
        f1();
        //第二种方式
        this.f1();
    }
}

```

4.访问构造器语法：this(参数列表); <u>注意只能在构造器中使用</u>

```java

package 面向对象_basic;

public class This {
    public static void main (String[] args) {
        T t1 = new T();
    }
}



class T {
    /*
    细节：访问构造器语法：this(参数列表);
    注意只能在构造器中使用，即只能在构造器中访问另外一个构造器

    注意：如果有 访问构造器语法：this(参数列表); 必须放在第一条语句
     */
    public T() {
        //这里去访问 T(String name, int age)
        this("jack",100);
        System.out.println("T() 构造器");
    }

    public T(String name, int age) {
        System.out.println("T(String name, int age) 构造器");
    }

}

```

5.this不能在类定义的外部使用，只能在类定义的方法中使用



### this 课堂小结

定义Person类，里面有name、age属性，并提供compareTo比较方法，用于判断是否和另一个人相等，提供测试类TestPerson用于测试，名字和年龄完全一样，就返回true，否则返回false

```java

package 面向对象_basic;

public class This {
    public static void main (String[] args) {
        Person p1 = new Person("marry",20);
        Person p2 = new Person("smith",30);
        System.out.println(p1.compareTo(p2));
        //p1是当前对象，this是p1
        //p2传给compareTo(Person p)里的p

    }
}


class Person {
    String name;
    int age;
    //构造器
    public Person (String name, int age) {
        this.name = name;
        this.age = age;
    }
    //
    public boolean compareTo(Person p) {
            return this.name.equals(p.name) && this.age == p.age;
        }
    }

```


## 本章作业

### 第一题

编写类A01，定义方法max，实现求某个double数组的最大值，并返回

```java

package 面向对象_basic;

public class Homework01 {
    public static void main (String[] args) {
       A01 a01 =  new A01();
       double[] arr = null;//{1.0,4.7,1.8};
       Double res = a01.max(arr);
       if(res != null) {
           System.out.println("arr的最大值=" + res);
       } else {
           System.out.println("arr的输入有误, 数组不能为null，或者{}");
       }
    }
}
/*
编写类A01，定义方法max，实现求某个double数组的最大值，并返回

思路分析
1 - 类名 A01
2 - 方法名 max
3 - 形参 (double[])
4 - 返回值 double

先完成正常的业务，再考虑优化代码
 */


class A01 {
    public Double max(double[] arr) {
        if(arr != null && arr.length > 0) {
        double max = arr[0]; //假定第一个元素就是最大值
        for(int i = 0; i < arr.length; i++) {
            if(max < arr[i]){
                max = arr[i];
            }
        }
        return max; //double
    } else {
            return null;
        }
    }
}

```


### 第二题

编写类A02，定义方法find，实现查找某字符串是否在字符串数组中，并返回索引，如果找不到，返回 -1

```java

package 面向对象_basic;

public class Homework02 {
    public static void main(String[] args) {
        String[] strs = {"harry", "anna", "tom"};
        A02 a02 = new A02();
        int index = a02.find("lily", strs);
        if(index != -1 ) {
            System.out.println("查找的index = " + index);
        } else {
            System.out.println("查找的index输入有误，数组不能为null/{}, 或者查找错误");
        } 

    }
}
/*
编写类A02，定义方法find，实现查找某字符串是否在字符串数组中，
并返回索引，如果找不到，返回 -1
 */
//分析
//1 - class名 A02
//2 - method名 find
//3 - 返回值 int
//4 - 形参(String, String[])

class A02 {
    public int find(String findStr,String[] strs) {
        if(strs != null && strs.length > 0) {
        //直接遍历字符串数组，如果找到，则返回下标/索引
        for(int i = 0; i < strs.length; i++) {
            if(findStr.equals(strs[i])) {
                return i;
            }
        }
        //如果没有，返回-1
        return -1;
        } else {
            return -1;
        }
    }
}

```


### 第三题

编写Book，定义方法updatePrice, 实现更改某本书的价格，具体：如果价格 > 150, 则更改为150， 如果价格 > 100, 更改为100，否则不变

```java

package 面向对象_basic;

public class Homework03 {
    public static void main(String[] args) {
        Book book = new Book("笑傲江湖",120);
        book.info();
        book.updatePrice(); //更新价格
        book.info();


    }
}
/*
编写Book，定义方法updatePrice, 实现更改某本书的价格，
具体：如果价格 > 150, 则更改为150， 如果价格 > 100, 更改为100，否则不变
*/
//分析
//1 - class名 Book
    //属性 price, name
//2 - method名 updatePrice
//3 - 返回值 void
//4 - 形参()
//5 - 提供一个构造器

class Book {
    String name;
    double price;
    public Book(String name, double price) {
        this.name = name;
        this.price = price;
    }
    public void updatePrice() {
        //如果方法中，没有price局部变量，this.price 等价 price
        if(this.price > 150) {
            this.price = 100;
        } else if (this.price > 100) {
            this.price = 100;
        }
    }
    //显示书籍的情况
    public void info() {
        System.out.println("书名=" + this.name + "价格=" + this.price);
    }
}

```



### 第四题

编写A03，实现数组的复制功能copyArr, 输入旧数组，返回一个新数组，元素和旧数组一样

```java

package 面向对象_basic;

public class Homework04 {
    public static void main(String[] args) {
        int[] oldArr = {10,20,30};
        A03 a03 = new A03();
        int[] newArr = a03.copyArr(oldArr);
        //遍历newArr, 验证
        for(int i = 0; i < newArr.length; i++) {
            System.out.print(newArr[i] + "\t");
        }

    }
}
/*
编写A03，实现数组的复制功能copyArr,
输入旧数组，返回一个新数组，元素和旧数组一样
*/
//分析
//1 - class名 A03
    //属性 price, name
//2 - method名 copyArr
//3 - 返回值 int[]
//4 - 形参(int[] oldArr)
//5 - 提供一个构造器

class A03 {
    public int[] copyArr(int[] oldArr) {
        //在堆中，创建了一个长度为oldArr.length的newArr数组
        int[] newArr = new int[oldArr.length];
        //遍历oldArr, 将元素拷贝到newArr
        for(int i = 0; i < oldArr.length; i++) {
            newArr[i] = oldArr[i];
        }
        return newArr;
    }
}

```



### 第五题

定义一个圆类Circle, 定义属性：半径，提供显示圆周长功能的方法，提供显示圆面积的方法

```java

package 面向对象_basic;

public class Homework05 {
    public static void main(String[] args) {
        Circle cir = new Circle(3);
        System.out.println("面积=" + cir.area() );
        System.out.println("周长=" + cir.len() );

    }
}
/*
定义一个圆类Circle, 定义属性：半径，提供显示圆周长功能的方法，提供显示圆面积的方法
*/

class Circle {
    double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    public double area() {
        return Math.PI * radius * radius;
    }

    public double len() {
        return 2 * Math.PI * radius;
    }

}

```

### 第六题

编程创建一个Cale计算类，在其中定义2个变量表示两个操作数，定义四个方法实现求和、差、乘、商（要求除数为0的话，要提示）并创建两个对象，分别测试

```java

package 面向对象_basic;

public class Homework05 {
    public static void main(String[] args) {
        Cale cale = new Cale(2,0);
        System.out.println("和=" + cale.sum());
        System.out.println("差=" + cale.minus());
        System.out.println("乘=" + cale.mul());
        Double divRes = cale.div();
        if (divRes != null) {
        System.out.println("商=" + cale.div());
        }
    }
}
/*
编程创建一个Cale计算类，在其中定义2个变量表示两个操作数，
定义四个方法实现求和、差、乘、商（要求除数为0的话，要提示）并创建两个对象，分别测试
*/

class Cale {
    double num1;
    double num2;

    public Cale(double num1, double num2) {
        this.num1 = num1;
        this.num2 = num2;
    }
    //和
    public double sum() {
        return num1 + num2;
    }
    //差
    public double minus() {
        return  num1 - num2;
    }
    //乘
    public double mul() {
        return  num1 * num2;
    }
    //商
    public Double div() {
        //判断
        if(num2 == 0) {
            System.out.println("num2不能为0");
            return null;
        } else {
            return num1 / num2;
        }
    }

}

```

### 第七题

设计一个Dog类，有名字、颜色和年龄属性，定义输出方法show()显示其信息，并创建对象，进行测试 【提示this.属性】


### 第八题

```java

class Test {
    int count = 9; //属性
    public void count1() { //Test类的成员方法
        count = 10;//这个count就是属性 改成10
        System.out.println("count1=" + count); //10
    }
    public void count2() { //Test类的成员方法
        System.out.println("count1=" + count++);//9 10
    }
    //这是main方法，任何一个类都可以有main 方法
    public static void main(String[] args) {
        //解读
        //1 - new Test() 是匿名对象，也就是没有返回没有名字的对象，匿名对象使用后就不能再使用（被销毁）
        //2 - new Test().count1(); 创建好匿名对象后，就调用count1()
        new Test().count1();
        Test t1 = new Test();
        t1.count2();
        t1.count2();

    }
}

```

![](https://tva1.sinaimg.cn/large/e6c9d24egy1gzmlt315zvj21im0r2tf3.jpg)


### 第九题

定义music类，里面有音乐名name, 音乐时长times属性，

并有播放play功能和返回本身属性信息的功能方法getInfo

```java

package 面向对象_basic;

public class Homework08 {

    public static void main(String[] args) {
        Music music = new Music("Hello", 300);
        music.play();
        System.out.println(music.getInfo());

    }
}
/*
定义music类，里面有音乐名name, 音乐时长times属性，
并有播放play功能和返回本身属性信息的功能方法getInfo
 */


class Music {
    String name;
    int times;
    public Music(String name, int times) {
        this.name = name;
        this.times = times;
    }
    //播放play功能
    public void play() {
        System.out.println("音乐" + name + "正在播放中... 时长为" + times + "秒");
    }
    //返回本身属性信息的功能方法getInfo
    public String getInfo() {
        return "音乐" + name + "播放时间为" + times;
    }

}

```

### 第十题

![](https://tva1.sinaimg.cn/large/e6c9d24egy1gzmmj5f4ilj21im0ri0xq.jpg)

```java

public class Homework09 {

    public static void main(String[] args) {

    }
}

class Demo {
    int i = 100;
    public void m() {
        int j=i++;
        System.out.println("i="+i); // 101
        System.out.println("j="+j); // 100
    }
}

class Test {
    public static void main(String[] args) { //运行它
        Demo d1 = new Demo();
        Demo d2 = d1;
        d2.m();
        System.out.println(d1.i); // 101
        System.out.println(d2.i); // 101
    }
}

```

### 第十一题

在测试方法中，调用method方法，代码如下，编译正确，试写出method方法的定义形式，调用语句为：System.out.println(method(method(10.0,20.0),100))

public double method(double d1, double d2) {...}


### 第十二题

创建一个Employee类，属性有（名字，性别，年龄，职位，薪水），提供3个构造器方法，可以初始化(1)(名字，性别，年龄，职位，薪水)，(2)(名字，性别，年龄)，(3)(职位，薪水)，要求充分复用构造器

```java

/*
创建一个Employee类，属性有（名字，性别，年龄，职位，薪水），
提供3个构造器方法，可以初始化(1)(名字，性别，年龄，职位，薪水)，(2)(名字，性别，年龄)，
(3)(职位，薪水)，要求充分复用构造器
 */

class Employee {
    //姓名 性别 年龄 职位 薪水
    String name;
    char gender;
    int age;
    String job;
    double sal;
    //因为要求可以复用构造器，因此先写属性少的构造器
    //职位 薪水
    public Employee(String job, double sal){
        this.job = job;
        this.sal = sal;
    }
    // 名字 性别 年龄
    public Employee(String name, char gender, int age){
        this.name = name;
        this.gender = gender;
        this.age = age;
    }
    // 名字 性别 年龄 职位 薪水
    public Employee(String job, double sal, String name, char gender, int age) {
        this(name, gender, age); //使用到 前面的 构造器
        this.job = job;
        this.sal = sal;
    }

}

```

### 第十三题

将对象作为参数传递给方法

题目要求

1.定义一个Circle类，包含一个double型的radius属性代表圆的半径，findArea()方法返回圆的面积

2.定义一个类PassObject, 在类中定义一个方法printAreas()，该方法的定义如下: public void printAreas(Circle c, int times) //方法签名/声明

3.在printAreas方法中打印输出1到times之间的每个整数半径值，以及对应的面积。例如，times为5，则输出半径1，2，3，4，5 以及对应的面积

4.在main方法中调用printAreas()方法，调用完毕后输出当前半径值。程序运行结果如图所示 (如果还是不明白，画内存图)

```java
package 面向对象_basic;

public class Homework09 {
    public static void main(String[] args) {
        Circle c = new Circle();
        PassObject po = new PassObject();
        po.printAreas(c,5);

    }
}

/*
1.定义一个Circle类，包含一个double型的radius属性代表圆的半径，findArea()方法返回圆的面积

2.定义一个类PassObject, 在类中定义一个方法printAreas()，该方法的定义如下:
    public void printAreas(Circle c, int times) //方法签名/声明

3.在printAreas方法中打印输出1到times之间的每个整数半径值，以及对应的面积。
    例如，times为5，则输出半径1，2，3，4，5 以及对应的面积

4.在main方法中调用printAreas()方法，调用完毕后输出当前半径值。程序运行结果如图所示
 */

class Circle {//class
    double radius;//属性 半径
    public Circle() {//默认无参构造器

    }
    public Circle(double radius) {
        this.radius = radius;
    }
    public double findArea() {//返回面积
        return Math.PI * radius * radius;
    }
    //添加方法setRadius，修改当前对象的半径值
    public void setRadius(double radius) {
        this.radius = radius;
    }

}

class PassObject {
    public void printAreas(Circle c, int times) {//输出1到times之间的每个整数半径值
        System.out.println("radius\tarea");
        for (int i = 1; i < times; i++) {
            c.setRadius(i);//修改c 对象的半径值
            System.out.println((double)i + "\t" + c.findArea());
        }
    }
}

```

### 第十四题

有个人Tom设计他的成员变量。成员方法，可以电脑猜拳

电脑每次都会随机生成0，1，2

0 表示 石头 / 1 表示 剪刀 / 2 表示 布

并要可以显示 Tom的输赢次数（清单）

```java
package 面向对象_basic;

import java.util.Random;
import java.util.Scanner;

/*
有个人Tom设计他的成员变量。成员方法，可以电脑猜拳

电脑每次都会随机生成0，1，2

0 表示 石头 / 1 表示 剪刀 / 2 表示 布

并要可以显示 Tom的输赢次数（清单）
 */
//测试类 主类
public class Guessing {
    //测试
    public static void main(String[] args) {
        //创建一个玩家对象
        Tom t = new Tom();
        //用来记录最后输赢的次数
        int isWinCount = 0;

        //创建一个二维数组，用来接收局部，Tom出拳情况以及电脑出拳情况
        int[][] arr1 = new int[3][3];
        int j = 0;

        //创建一个一维数组，用来接收输赢情况
        String[] arr2 = new String[3];

        Scanner scanner = new Scanner(System.in);
        for (int i = 0; i < 3; i++) { //比赛3次
            //获取玩家出的拳
            System.out.println("输入你要出的拳头（0-拳头 1-剪刀 2-布）");
            int num = scanner.nextInt();
            t.setTomGuessNum(num);
            int tomGuess = t.getTomGuessNum();
            arr1[i][j+1] = tomGuess;

            //获取电脑出的拳
            int comGuss = t.computerNum();
            arr1[i][j+2] = comGuss;

            //将玩家猜的拳与电脑做比较
            String isWin = t.vsComputer();
            arr2[i] = isWin;
            arr1[i][j] = t.count;

            //对每一局的情况进行输出
            System.out.println("==================");
            System.out.println("局数\t玩家的出拳\t电脑的出拳\t输赢情况");
            System.out.println(t.count + "\t" + tomGuess + "\t\t" + comGuess + "\t\t");
            																//这里的comGuss有点问题
            System.out.println("==================");
            System.out.println("\n\n");
            isWinCount = t.winCoun(isWin); //这里的winCoun有点问题
        }

        //对游戏的最终结果进行输出
        System.out.println("局数\t玩家的出拳\t电脑的出拳\t\t输赢的情况");
        for(int a = 0; a < arr1.length; a++) {
            for (int b = 0; b < arr1[a].length; b++) {
                System.out.println(arr1[a][b] + "\t\t\t");
            }
            System.out.println(arr2[a]);
            System.out.println();
        }
        System.out.println("你赢了" + isWinCount + "次");


    }
}


//Tom类
class Tom { //核心代码
    //玩家出拳类型
    int tomGuessNum; //0 1 2
    //电脑出拳的类型
    int comGuessNum; //0 1 2
    //玩家赢的次数
    int winCountNum;
    //比赛的次数
    int count = 1;//一共比赛3次

    public void showInFo() {
        //...
    }

    /**
     * 电脑随机生成猜拳数字的方法
     * @return
     */

    public int computerNum() {
        Random r = new Random();
        comGuessNum = r.nextInt(3); //方法 返回0-2的随机数
        //System.out.println(comGuessNum);
        return comGuessNum;
    }

    /**
     * 设置玩家猜拳的数字的方法
     * @param tomGuessNum
     */

    public void setTomGuessNum(int tomGuessNum) {
        if (tomGuessNum > 2 || tomGuessNum < 0) {
            //抛出一个异常，李同学会写，没有处理
            throw new IllegalArgumentException("数字输入错误");
        }
        this.tomGuessNum = tomGuessNum;
    }

    public int getTomGuessNum() {
        return tomGuessNum;
    }

    /**
     * 比较猜拳的结果
     * @return 玩家赢返回true，否则返回false
     */

    public String vsComputer() {
        //比较巧
        if(tomGuessNum == 0 && comGuessNum == 1 ) {
            return "你赢了";
        } else if (tomGuessNum == 1 && comGuessNum == 2) {
            return "你赢了";
        } else if (tomGuessNum == 2 && comGuessNum == 0) {
            return "你赢了";
        } else if (tomGuessNum == comGuessNum) {
            return "平手";
        } else {
            return "你输了";
        }

    }

    /**记录玩家赢的次数
     * @return
     */
    
    public int winCount(String s) {
        count++;
        if (s.equals("你赢了")) { //统计赢的次数
            winCountNum++;
        }
        return winCountNum;
    }
}


```






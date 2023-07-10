# 001 java语法学习
## java的特点

 - java支持跨平台运行
 - java编译为字节码，jvm通过字节码运行
 - 源代码（.java）->字节码（.class）->执行
## java的练习（99数到0）

```java
public class num{
	public static void main(String argu[]){
		for(int i = 99;i >= 0; i = i - 1){
			System.out.println(i);
		}
	}
}
```
## 类的初步学习

 - 类是对象的蓝图
 - java没有全局变量，带有static和public可是互相存取
## 数据类型
 - 基本数据类型
 	- 8种基本数据类型（boolean、int、double、long、char、byte、short、float）
 	- char是两个字节
 	- 命名必须字母、下划线或$
 - 对象类型
	- 对象的引用变量只保留地址，同一个jvm下大小一样
	
 	- 引用不能参与计算，不同于c
 	- 引用可以指向同类的不同对象，而不能指向不同类的对象
 	- 引用可以多对一，没有被引用的对象（null）会被回收

	

```java
// 创建一个类的实例化
Dog mydog1 = new Dog();
// new 关键词开辟了对象的空间
// Dog 关键词声明了一个对象引用
```
# 002 数组

 - int数组的创建

```java
// 创建数组
int[] nums = new int[10];
// new--开辟了10个int的数组存储空间
// 数组名为nums
nums[0] = 11;
// 给数组元素赋值
```

 - 引用变量数组的创建
 

```java
Dog[] pets = new Dog[5];
// 创建了5个引用对象的数组，实际的对象没有创建，也没有设置指向的地址
Dog[0] = new Dog();
```
# 003 面向对象进阶

 - 类的方法学习

```java
public class Test{
	//测试dog类不同情况实现功能有区别
	public static void main(String[] args){
	Dog mydog = new Dog();
	mydog.weight = 12;
    mydog.bark();
	}
}

class Dog{
	int name;
	int weight;
	
	public void bark(){
		if (weight > 10){
			System.out.print("big");
		}
		else{
			System.out.print("small");
		}
	}
}
	
```

 - 类的方法——传参
	 - java的参数传递是拷贝传递的，形参保留实际数据并非地址，形参和实参无关系，，不会相互更新
	 - java传递引用参数是类似的，拷贝了引用
	 - 传递返回值只能返回一个，实在想传多个就传递数组
 

```java
public class Test{
	public static void main(String[] args){
	Dog mydog = new Dog();
    mydog.bark(12);
	}
}

class Dog{
	public void bark(int times){
		while(times > 0){
			System.out.println("hello");
			times = times - 1;
		}
	}
}
	
```
## 封装

 - 不要让类的名称暴露
 - 使用类的方法进行参数的存取
 ## 数据保护
 
 - private修饰符
 - setter和getter

```java
// 封装
class Test{
	public static void main(String[] args){
		Dog myDog = new Dog();
		myDog.bark();
		myDog.setName("ryan");
		myDog.setWeight(10);
		myDog.bark();
		System.out.println(myDog.getName());
		System.out.println(myDog.getWeight());
	}
}
class Dog{
	private String name;
	private int weight;
	void bark(){
		System.out.println(name + " is barking!");
	}
	String getName(){
		return name;
	}
	int getWeight(){
		return weight;
	}
	void setName(String setName){
		name = setName;
	}
	void setWeight(int setWeight){
		weight = setWeight;
	}
}
```

## 局部变量和实例变量
 - 局部变量
 没有默认值（0或者null），会直接编译不通过
 
 - 实例变量
 有默认值（0，0.0，null，false）
## 判断相等
 - == 用来判断基本数据类型是否相等
 - equals()判断引用的对象意义是否相同

# 004 ArrayList类

 - 应该是类似链表的结构
 - 方法有：add、remove、contains、isEmpty、indexOf、size、get
```java
import java.util.ArrayList;

public class Test{
	public static void main(String[] args){
		ArrayList<Integer> myList = new ArrayList<Integer>();
		myList.add(12);             //加入元素12
		myList.add(19);             //加入元素19
		myList.remove(0);       //移除索引为0的元素
		System.out.println(myList.contains(12));//检查12有没有被删除
		System.out.println(myList.contains(19));//检查19是否存在
		System.out.println(myList.isEmpty());	//检查是否为空
		System.out.println(myList.indexOf(19)); //查找元素19的索引
		System.out.println(myList.size()); //输出大小
		System.out.println(myList.get(0)); //输出索引0的数据
//输出
/*
false
true 
false
0    
1    
19
 */
	}
}
```
# 005 函数库（Java Api）

 - import和include不同，import不会增加代码大小
 - java lang是基础包，包括基本类、System等
 - 查找Api在线官方文档[#点击我#](https://www.oracle.com/java/technologies/)
# 006 类的高级运用——继承和多态
 - 继承就是创建一个父类，生成一堆子类
 - 关键词 extends

```java
class Test{
	public static void main(String[] args){
		Dog mydog = new Dog();
		mydog.roam();
		Hippo myHippo = new Hippo();
		myHippo.roam();
	}
}
class Animal{
	int picture;
	int food;
	int hunger;
	int bondaries;
	int location;
	void makeNoise(){
		//do nothing
	}
	void eat(){
		//eat
	}
	void sleep(){
		//sleep
	}
	void roam(){ 
		System.out.println("I don't konw");    //属于什么科的动物
	}
}
//猫科动物的类
class Feline extends Animal{
	void roam(){
		System.out.println("I am feline");
	}
}
//犬科动物的类
class Cannine extends Animal{
	void roam(){
		System.out.println("I am cannine");
	}
}
//河马
class Hippo extends Animal{
	void makeNoise(){
		System.out.println("henghengheng");
	}
	void eat(){
		System.out.println("I eat grass");
	}
}
class Dog extends Cannine{
	void makeNoise(){
		System.out.println("woff");
	}
	void eat(){
		System.out.println("I eat bone");
	}
	
}
```

 - 属于同一父类的个子类可以用同一个引用类型，就是多态的概念
 - final修饰类可以让类不能继承，final修饰方法可以让该方法不被覆盖
 - 子类**方法覆盖**的规则
	 - 覆盖的函数必须不能改变输入参数，返回类型也必须兼容
	 - 不能降低存取权限，如改用私有是错误的
 - 子类**方法重载**的规则
	 - 重载的方式是两个方法名称相同，参数不同，重载与多态无关
	 - 返回类型可以不同
	 - 但是不能只是返回类型不同，参数也要是不同的
	 - 可以修改存取权限
```java
// 给setName方法扩展，int和string都可以作为参数输入
class Test{
	public static void main(String[] args){
		Dog myDog = new Dog();
		myDog.setName(123);
		myDog.showName();
	}
}
class Dog{
	String name;
	void setName(String setname){
		name = setname;
	}
	void setName(int setName){
		name = String.valueOf(setName);
	}
	void showName(){
		System.out.println(name);
	}
}
```
# 007 接口——多态的重点
 - 抽象类：关键词abstract，放在class前，表示抽象类无法被初始化
 - 抽象的class可以有static成员，没有其他用途，不能实例化
 - 方法也可以被抽象，表示该方法必须被覆盖才行
 - 所有类的父类——Object

```java
// Object类的展示
class Test{
	public static void main(String[] args){
		//
		Dog myDog = new Dog();
		myDog.setName("kk");
		myDog.showName();
		Cat myCat = new Cat();
		myCat.setName("nono");
		myCat.showName();
		System.out.println(myCat.equals(myCat));
		System.out.println(myCat);
		System.out.println(myCat.hashCode());
		System.out.println(myCat.getClass());
		System.out.println(myCat.toString());
	}
}
class Dog{
	String name;
	void setName(String setname){
		name = setname;
	}
	void showName(){
		System.out.println(name);
	}
}
class Cat{
	String name;
	void setName(String setname){
		name = setname;
	}
	void showName(){
		System.out.println(name);
	}
}
```

 - Object类部分方法可以覆盖
 ## 多重继承
 
 - 解决了分属多个类的问题
 - 但引用致命方块问题：继承的多个类的方法有冲突
 - 所以Java实际上不允许多重继承
 - 解决：接口
 ## 接口
 
 - 接口是100%的抽象类，接口方法必须全部抽象，方法都要重写，避免继承冲突
 - 接口关键词，interface，替换class
 - 使用接口implements关键字
 - 有了接口，便于实现多态，能继承超级多的来源

```java
public class Test{
	public static void main(String[] args){
		Petdog myPetdog = new Petdog();
		myPetdog.play();
	}
}
class Petdog extends Dog implements pet{
	public void play(){
		System.out.println("haha");
	} 
}
class Dog{
	String name;
	void setName(String setname){
		name = setname;
	}
	void showName(){
		System.out.println(name);
	}
}
public interface pet{
	public abstract void play();
}
```
# 008 构造器和垃圾回收

 - 构造函数一定有，没有的话编译器也会写一个空语句的构造函数
 - 构造函数在类中，与类同名
 - 构造函数没有返回值，声明时不用说明返回值类型
 - 构造函数不被继承

```java
// 用构造函数进行初始化
public class Test{
	public static void main(String[] args){
		Dog myDog = new Dog();
		myDog.showData();
	}
}
class Dog{
	int age;
	String name;
	public Dog(){
		age = 0;
		name = "bao";
	}
	void showData(){
		System.out.println(age);
		System.out.println(name);
	}
}
```

 - 构造函数也可重载增强扩展性
 - new一个子类，自动调用父类的构造函数，不是父类名称()，而是super()
 - 子类对父类的构造函数重构，可以用this()先调用自己类真正的构造函数，减少代码量

## 对象的生命周期
 - 局部变量只会存在他声明的方法中
 - 实例变量的寿命和对象相同
![在这里插入图片描述](https://img-blog.csdnimg.cn/img_convert/3ba5b44fc5058e41f64a0b235041dc80.png#pic_center)
 - 对象的所有引用消失了，对象会被回收
 	三种回收的方法：
 	- 对象的创建在一个方法内，方法结束，引用释放
 	- 对象引用被赋值其他对象，原对象失去唯一的引用
 	- 对象引用被设置为null
 
## 静态
 - 静态的方法，不会有实例化
 - 静态方法用类来调用
 - 静态变量，对类是共享的，只会在第一次新建时初始化
 - 静态变量会在创建类之前就初始化
 - 静态变量会在类的静态方法执行前就初始化
 - 静态变量被final修饰将是常量（常量命名应该是全大写）
 

```java
public class Main{
    public static void main(String[] args){
        Dog.bark();//没有实例化调用了静态方法
        System.out.println(Dog.barkTimes);
    }
}
class Dog{
    static int barkTimes = 0;
    static void bark(){
        System.out.println("woof");
        barkTimes ++;
    }
}
```
# 009 数据类型

 - 类型转换

```java
// String转int
public class Main{
    public static void main(String[] args){
        int sum;
        String number = "12";
        sum = Integer.parseInt(number);
        System.out.println(sum);
    }
}
```

 

```java
//int转String
public class Main{
    public static void main(String[] args){
        int sum = 1;
        String string = "" + sum;
        System.out.println(string);
    }
}
```

 - Calendar Api

```java
import java.util.Calendar;

public class Main{
    public static void main(String[] args){
        Calendar c = Calendar.getInstance(); //创建时间实例
        System.out.println(c.getTime());     //默认为电脑当前时间
        c.set(2001,2,22,22,22);
        System.out.println(c.getTime());
        c.add(0,6);
        System.out.println(c.getTime());
        System.out.println(c.get(1));
        System.out.println(c.getTimeInMillis());
        System.out.println(c.getTime());
    }
}
```
# 异常处理

```java
public class Main{
    public static void main(String[] args){
        Dog myDog = new Dog();
        myDog.life = false;
        try{
            myDog.takeRisk();
        }catch (Waring ex){
            System.out.println("bad");
            ex.printStackTrace();
        }
    }
}
class Dog{
    public boolean life = true;
    public void takeRisk() throws Waring{
        if (!life){
            throw new Waring();
        }
    }
}
class Waring extends Exception{

}


```

 - 异常时Exception类及其所有子类
 - 除了RuntimeException及其子类触发异常不会被编译器注意，其他都会响应
 - 当运行的代码包含有异常的可能就要用try，catch语句包裹
 - try，catch后可加finally块语句，保持正常和异常都要执行的语句

```java
// ducking忽略掉异常
public class Main{
    public static void main(String[] args)throws Waring{
        Dog myDog = new Dog();
        myDog.life = false;
        myDog.takeRisk();
    }
}
class Dog{
    public boolean life = true;
    public void takeRisk() throws Waring{
    }
}
class Waring extends Exception{

}
```
## 音乐播放器

```java
import javax.sound.midi.*;

public class Main{
    public static void main(String[] args) throws Exception {
        Main minimusicplayer = new Main();
        minimusicplayer.play();
    }
    public void play() throws Exception {
        try{
            Sequencer player = MidiSystem.getSequencer();
            player.open();
            Sequence seq = new Sequence(Sequence.PPQ,4);
            Track track = seq.createTrack();

            ShortMessage a = new ShortMessage();
            a.setMessage(144,1,44,100);
            MidiEvent noteOn = new MidiEvent(a,1);
            track.add(noteOn);

            ShortMessage b = new ShortMessage();
            b.setMessage(128,1,44,100);
            MidiEvent noteOff = new MidiEvent(b,16);
            track.add(noteOff);

            player.setSequence(seq);

            player.start();
        } catch (Exception e) {
                throw new Exception(e);
        }
    }
}
```

```java
import javax.sound.midi.*;


public class MiniMiniMusicCmdLine {   // this is the first one
       
     public static void main(String[] args) {
        MiniMiniMusicCmdLine mini = new MiniMiniMusicCmdLine();
        if (args.length < 2) {
            System.out.println("Don't forget the instrument and note args");
        } else {
            int instrument = Integer.parseInt(args[0]);
            int note = Integer.parseInt(args[1]);
            mini.play(instrument, note);
            
        }
     }

    public void play(int instrument, int note) {

      try {
 
         Sequencer player = MidiSystem.getSequencer();         
         player.open();
        
         Sequence seq = new Sequence(Sequence.PPQ, 4);         
         Track track = seq.createTrack();  
          
         MidiEvent event = null;

         ShortMessage first = new ShortMessage();
         first.setMessage(192, 1, instrument, 0);
         MidiEvent changeInstrument = new MidiEvent(first, 1); 
         track.add(changeInstrument);

         
         ShortMessage a = new ShortMessage();
         a.setMessage(144, 1, note, 100);
         MidiEvent noteOn = new MidiEvent(a, 1); 
         track.add(noteOn);

         ShortMessage b = new ShortMessage();
         b.setMessage(128, 1, note, 100);
         MidiEvent noteOff = new MidiEvent(b, 16); 
         track.add(noteOff);
         player.setSequence(seq); 
         player.start();
         // new
	     Thread.sleep(5000);
	     player.close();
         System.exit(0);

      } catch (Exception ex) {ex.printStackTrace();}
  } // close play

} // close class
```

 - 控制台运行

用控制台编译： javac Test.java
运行： Java Test aaa bbb ccc
记得运行那一行代码后面带上三个参数~~~参数之间用空格隔开！
# 010 图形接口

```java
import javax.swing.*;
import java.awt.event.*;

public class Main implements ActionListener {
    JButton button;
    public static void main(String[] args){
        Main main = new Main();
        main.go();
    }
    public void go(){
        JFrame frame = new JFrame();
        button = new JButton("Click me");

        button.addActionListener(this);

        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.getContentPane().add(button);
        frame.setSize(300,300);
        frame.setVisible(true);
    }
    public void actionPerformed(ActionEvent event){
        button.setText("ok");
    }
}


```
## 绘制图形

```java
import java.awt.*;
import javax.swing.*;

public class Main extends JPanel {
    public static void main(String[] a) {
        JFrame f = new JFrame();
        f.setTitle("实心的矩形");
        f.setSize(400, 400);
        f.add(new Main());
        f.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        f.setVisible(true);
    }

    public void paint(Graphics g) {
        g.setColor(Color.orange);
        g.fillRect(20, 50, 100, 100);
    }
}

```
## 绘制jpg

```java
import java.awt.*;
import javax.swing.*;

public class Main extends JPanel {
    public static void main(String[] a) {
        JFrame f = new JFrame();
        f.setTitle("实心的矩形");
        f.setSize(400, 400);
        f.add(new Main());
        f.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        f.setVisible(true);
    }

    public void paint(Graphics g) {
    // 路径修改
        Image image = new ImageIcon("D:\\Ryan\\OneDrive - csu.edu.cn\\圆宝\\nx2000\\2023-04-29\\select\\SAM_0061.JPG").getImage();
                g.drawImage(image,3,4,this);
    }
}

```
## 绘制随机颜色的圆

```java
import java.awt.*;
import javax.swing.*;

public class Main extends JPanel {
    public static void main(String[] a) {
        JFrame f = new JFrame();
        f.setTitle("设置一个标题");
        f.setSize(400, 400);
        f.add(new Main());
        f.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        f.setVisible(true);
    }

    public void paint(Graphics g) {
        g.fillRect(0,0,this.getWidth(),this.getHeight());

        int red = (int)(Math.random()*255);
        int green = (int)(Math.random()*255);
        int blue = (int)(Math.random()*255);

        Color randomColor = new Color(red,green,blue);
        g.setColor(randomColor);
        g.fillOval(70,70,100,100);
    }
}

```
## 点击按钮绘制不同颜色的圆

```java
import javax.swing.*;
import java.awt.event.*;
import java.awt.*;

public class Main implements ActionListener {
    JFrame frame;
    public static void main(String[] args){
        Main main = new Main();
        main.go();
    }
    public void go(){
        frame = new JFrame();
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        JButton button = new JButton("change colors");
        button.addActionListener(this);

        MyDrawPanel drawPanel = new MyDrawPanel();

        frame.getContentPane().add(BorderLayout.SOUTH,button);
        frame.getContentPane().add(BorderLayout.CENTER,drawPanel);
        frame.setSize(300,300);
        frame.setVisible(true);
    }
    public void actionPerformed(ActionEvent event){
        frame.repaint();
    }
}
class MyDrawPanel extends JPanel{
    public void paintComponent(Graphics g){
        g.fillRect(0,0,this.getWidth(),this.getHeight());

        int red = (int)(Math.random()*255);
        int green = (int)(Math.random()*255);
        int blue = (int)(Math.random()*255);

        Color randomColor = new Color(red,green,blue);
        g.setColor(randomColor);
        g.fillOval(70,70,100,100);
    }
}
```
## 内部类

 - 一个类可以嵌套在类的内部
 - 内部类可使用外部所有方法及变量，包括私有的

```java
import javax.swing.*;
import java.awt.event.*;
import java.awt.*;

public class Main {
    JFrame frame;
    JLabel label;

    public static void main(String[] args){
        Main main = new Main();
        main.go();
    }
    public void go(){
        frame = new JFrame();
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        JButton labelButton = new JButton("change label");
        labelButton.addActionListener(new LabelListener());

        JButton colorButton = new JButton("change colors");
        colorButton.addActionListener(new ColorListener());

        label = new JLabel("I'm a label");
        MyDrawPanel drawPanel = new MyDrawPanel();

        frame.getContentPane().add(BorderLayout.SOUTH,colorButton);
        frame.getContentPane().add(BorderLayout.CENTER,drawPanel);
        frame.getContentPane().add(BorderLayout.EAST,labelButton);
        frame.getContentPane().add(BorderLayout.WEST,label);
        frame.setSize(300,300);
        frame.setVisible(true);
    }
    public void actionPerformed(ActionEvent event){
        frame.repaint();
    }
    class LabelListener implements ActionListener{
        public void actionPerformed(ActionEvent event){
            label.setText("ouch!");
        }
    }

    class ColorListener implements ActionListener{
        public void actionPerformed(ActionEvent event){
            frame.repaint();
        }
    }
}
class MyDrawPanel extends JPanel{
    public void paintComponent(Graphics g){
        g.fillRect(0,0,this.getWidth(),this.getHeight());

        int red = (int)(Math.random()*255);
        int green = (int)(Math.random()*255);
        int blue = (int)(Math.random()*255);

        Color randomColor = new Color(red,green,blue);
        g.setColor(randomColor);
        g.fillOval(70,70,100,100);
    }

}
```


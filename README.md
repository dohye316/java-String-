# java-String-
String类使用
包装类的分类     String类的使用  ；Integer包装类的使用；
1.针对八种基本定义相应的引用类型-包装类
2.有了类的特点，就可以调用类中的方法
基本数据类型                    包装类
boolean                           Boolean
char                                Character
byte                                Byte
short                                 Short
int                                 Integer
long                              Long
float                                  Float
double                           Double
Wrapper包装类
基本数据包装类是Number的子类，Number是Object的子类，
基本数据的interface是Comparable
Number的interface是Serializable  

包装类和基本数据类型的转换
演示：包装类和基本数据类型的相互转换，这里以int和Integer演示
1.jdk5前的手动装箱和拆箱方式，装箱：基本类型-》包装类型，反之，拆箱
2.jdk5以后（含jdk5）的自动装箱和拆箱方式
3.自动装箱底层调用的是valueOf方法，比如Integer.valueOf()

三元运算符是一个整体，一真大师，







=======================================
Integer的包装拆箱
public class Integer01 {
    public static void main(String[] args) {
        //演示int<==>Integer的装箱和拆箱
        //jdk5以前是手动装箱和拆箱
        //手动装箱
        int n1 =100;
        Integer integer = new Integer(n1);
        Integer integer1=Integer.valueOf(n1);
        // public static Integer valueOf(int i) {
        //        if (i >= IntegerCache.low && i <= IntegerCache.high)
        //            return IntegerCache.cache[i + (-IntegerCache.low)];
        //        return new Integer(i);注意！！！地址相同
        //    }
        //手动拆箱
        //Integer->int
        int i= integer.intValue();
        int j =integer1.intValue();
        //jdk5后，就可以自动装箱
        int n2 = 200;
        Integer integer2 = n2;//底层使用的是new Integer.valueOf(n2)
        //自动拆箱
        int n3 = integer2;
    }
}













================================

String类型的包装

public class WrapperVSString {
    public static void main(String[] args) {
        //包装类（Integer）-》String
        Integer  i = 100;//自动装箱
        //方式1
        String  str1 = i + "";
        //方式2
        String s = i.toString();
        //方式3
        String s1 = String.valueOf(i);
        //String ->包装类（Integer）
        String str4 = "123456";
        Integer i2 = Integer.parseInt(str4);//使用到自动装箱
        Integer integer = new Integer(str4);
        
    }
}

======================================


public class Wrapper {
    public static void main(String[] args){
    Integer i = new Integer(1);
    Integer j = new Integer(1);
        System.out.println(i == j);
        Integer m = 1;//integer.valueOf
        Integer n = 1;//integer.valueOf
        System.out.println(m == n);
        Integer x = 128;//主要看范围 -128 ~127就是直接返回，不是这个范围的new一个地址
        Integer y = 128;
        System.out.println(x == y);
        Integer integer = Integer.valueOf(5);
        /**
         *       * This method will always cache values in the range -128 to 127,
         *      * inclusive, and may cache other values outside of this range.
         *      *
         *      * @param  i an {@code int} value.
         *      * @return an {@code Integer} instance representing {@code i}.
         *      * @since  1.5
         *      */
        //如果 i在这些范围内，就直接从数组返回
        //如果不在这些范围，就直接new Integer
//         *public static Integer valueOf ( int i){
//         *if (i >= Integer.IntegerCache.low && i <= IntegerCache.high)
//         *return IntegerCache.cache[i + (-IntegerCache.low)];
//         *return new Integer(i);
//         *}
//         */
//f f  t f f tt
        
          Integer i11 = 127;
          int i12 = 127;
        System.out.println(i11 == i12);//T
        //解释只要有基本数据类型则比较的对象是值

    }
}

常用类：
String
1.String对象用于保存字符串，也就是一组字符序列
2.字符串常量对象是用双引号括起来的字符序列，例如：“你好”，“12.9”
3.字符串的字符使用Unicode字符编码，一个字符（不区分字母还是汉子）占两个字节
4.String类较常用的构造器
String s1 = new String ();
String s2 = new Strign ();


public class String01 {
    public static void main(String[] args) {
        //1.String 对象用于保存字符串
        //一个字符占两个字节
        //Sting有很多构造器
        //常用的有String s1 = new String();
        //String s2 = new String(Strign original);
        //String s3 = new String (char[]a);
        //String s4 = new String (cahr[] a,int startIndex,int count);
        //String s5 = new String (byte[]b)
        //5.String类实现了接口Serializable【Sting可以串行化，可以在网络传输】
        //还有comparable接口 compareto【String 对性可以比较大小】
        //还有value【】
        //6.String 是final类，不能被其他的类继承
        //7.String 有属性 private final char value[]; 用于存放字符串内容
        //8.一定要注意：value是一个final类型，不可以修改,指的是地址不能修改
        //新的地址，但是单个字符内容是可以变化
        final char value[]= {'a','b','c'};
        value[0]='H';
        String name ="jack";
        name = "tom";//地址不能修改里面的值能修改
         char[] v2 ={'t','o','m'};
       //value = v2; 不可以修改value地址

    }
}

-===============================

两种创建String对象的区别
方式一：直接赋值String s = "hsp";
方式二：调用构造器 String s2 = new String ("hsp);
1.方式一：先从常量池查看是否有“hsp”数据空间，如果有，直接指向；如果没有则重新创建，然后指向，s最终指向的是常量池的空间地址
2.方式二：先在堆中创建空间，里面维护了value属性，指向常量池的hsp空间。
如果常量池没有“hsp”，重新创建，如果有，直接通过value指向。最终指向的是堆中的空间地址
3.画出两种方式的内存分布图

String本质是char的数组


public class String01 {
    public static void main(String[] args) {
        //1.String 对象用于保存字符串
        //一个字符占两个字节
        //Sting有很多构造器
        //常用的有String s1 = new String();
        //String s2 = new String(Strign original);
        //String s3 = new String (char[]a);
        //String s4 = new String (cahr[] a,int startIndex,int count);
        //String s5 = new String (byte[]b)
        //5.String类实现了接口Serializable【Sting可以串行化，可以在网络传输】
        //还有comparable接口 compareto【String 对性可以比较大小】
        //还有value【】
        //6.String 是final类，不能被其他的类继承
        //7.String 有属性 private final char value[]; 用于存放字符串内容
        //8.一定要注意：value是一个final类型，不可以修改,指的是地址不能修改
        //新的地址，但是单个字符内容是可以变化
        final char value[]= {'a','b','c'};
        value[0]='H';
        String name ="jack";
        name = "tom";//地址不能修改里面的值能修改
         char[] v2 ={'t','o','m'};
       //value = v2; 不可以修改value地址



        String a ="hsp";//a指向 常量池的“hsp”
        String b = new String("hsp");
        System.out.println(a.equals(b));//T，b指向堆中的对象
        System.out.println(a == b);//F
        System.out.println(a == b.intern());//T
        System.out.println(b == b.intern());//F
         //当调用intern方法时，如果池已经包含一个等于此String对象的字符串，(用equals（Object）方法确定)则返回池中的字符串。否则，将此String对象添加到池中
//并返回此String对象的引用
        //老韩解读：1.b.intern()方法最终返回的是常量池的地址。
       String s1 = "hspedu";
       String s2 = "java";
       String s4 = "java";
       String s3 = new String ("java");
        System.out.println(s2 == s3);//f
        System.out.println(s2 == s4);//t
        System.out.println(s2.equals(s3));//t
        System.out.println(s1 == s2);//f
        Person p1= new Person();
        p1.name ="hspedu";
        Person p2= new Person();
        p2.name ="hspedu";
        System.out.println(p1.name == p2.name);//t
        System.out.println(p1.name == "hspedu");//t

    }

1.String是一个final类，代表不可变得字符序列
2.字符串是不可变得。一个字符串对象一旦被分配，其内容是不可变得。
以下语句创建了几个对象？
String s1 = “hello”；
s1 = “哈哈“；
//创建了2个对象
String a = “hello” + “abc”；
创建了几个对象：一个  等价于String a = “helloabc”
String a = "hello";
String b = "abc";
String c = a+ b;
创建了几个对象： 三个
  String a = "hello";
        String b = "abc";
        //1.先创建一个StringBuilder sb = StringBuilder()
        //2.执行sb.append("hello)
        //3.sb.append("abc")
        //4.String c =sb.toString()
        //最后其实是 c指向堆中的对象（String ）value【】-》池中“helloabc”
        String c = a+b;//一共3个对象
        String d = "helloabc";
        System.out.println(c == d);//F
 String e = "hello" + "abc";
        System.out.println(e == d);//T
        //字符串常量相加直接看池，e指向常量池

//底层是StringBuilder sb = new StringBuilder(); sb.append(a);
sb.append(b);sb是在堆中，并且append是在原来字符串的基础上追加的。
重要规则，String c1 = "ab" + "cd"; 常量相加，看的是池。 String c1 = a+b; 变量相加，是在堆中
===============================
intern访问池中的常量
  String s1 ="hspedu";
        String s2 = "java";
        String s5 = "hspedujava";
        String s6 = (s1 = s2).intern();
        System.out.println(s5 == s6);//T
        System.out.println(s5.equals(s6));//T


=====================================
public class String02 {//尝试画出内存布局图
    public static void main(String[] args) {
        String s1 ="hspedu";
        String s2 = "java";
        String s5 = "hspedujava";
        String s6 = (s1 = s2).intern();
        System.out.println(s5 == s6);//T
        System.out.println(s5.equals(s6));//T

    }
}
class Test {
    String str = new String("hsp");
    final char[] ch = {'j', 'a', 'v', 'a'};

    public void change(String str, char ch[]) {
        str = "java";
        ch[0] = 'h';
    }


    public static void main(String[] args) {
        Test ex = new Test();
        ex.change(ex.str, ex.ch);
        System.out.println(ex.str + "and");
        System.out.println(ex.ch);
        //hspandhava
    }
}

String常用方法
String类是保存字符串常量的，每次更新都需要重新开辟空间，效率较低，因此java设计者还提供了StringBuilder和StringBuffer来增强String的功能
并提高效率。
String s = new String ("");
for(int i = 0; i < 80000; i++){
s+="hello";}
public class StringUML {
    public static void main(String[] args) {
   //String常用方法
        /**
         * equals //区分大小写，判断内容是否相等
         * equalsIgnoreCase//忽略大小写的判断内容是否相等
         * length//获取字符的个数，字符串的长度
         * indexOf//获取字符在字符串中第一次出现的索引，索引从0开始，如果找不到，返回-1
         * lastindexOf//获取字符在字符串中最后1次出现的索引，索引从0开始，如找不到，返回-1
         * substring //截取指定范围的子串
         * trim//去前后空格
         * charAt:获取某索引处的字符，注意不能使用Str【index】这种方式。
         *
         */
        String str ="hello";
        //str[0]不对
        str.charAt(0); //对
        String username = "johN";
        if ("john".equalsIgnoreCase(username)){
            System.out.println("Success!");//Success
        }else{
            System.out.println("Failure!");
        }
        System.out.println("韩孙平".length());3
        String s1 ="flower";
        int index = s1.indexOf('f');0//第一次出现这个字母或字节的序号
        System.out.println(index);
        String name ="hello,张三";
        System.out.println(name.substring(6));//截取后面的字符，张三
        //下面name.substring6开始从索引6开始截取后面所有的内容
        System.out.println(name.substring(2, 5));llo
       System.out.println(s1.lastIndexOf("ow"));

    }
}



        //String类的常见方法应用实例2
        /**
         * 看老师的案例演示第二组String相关的方法：
         * toupperCase
         * toLovwerCase
         * concat
         * raplace提花字符串中的字符
         * split 分割字符串，对于某些峰字符，我们需要转义比如|\\等
         * 案例“ Stringpoem = ”锄禾日当午，汗滴禾下土，谁知盘中餐，粒粒皆辛苦“；和 文件路径
         * compareTo//比较两个字符串的大小
         * toCharArray//转换成字符数组
         * format//格式字符串，%s字符串%c字符%d整型%2f浮点型
         * 案例，将一个人的信息格式化输出
         *
         */


        String s ="hello";
        System.out.println(s.toUpperCase());//HELLO
        System.out.println(s.toLowerCase());//hello
        //concat拼接字符串
        System.out.println(s = s.concat("dds").concat("fff").concat("pp"));
        String s6="暴雨and 林黛玉 皮包差";

//        s6 = s6.replace("林","暴雨");
        String s11= s6.replace("林","暴雨");
        //s6.replace（）方法执行后，返回的结果才是替换过的，
        //本身对s1没有任何影响
        System.out.println(s6);//暴雨and 林黛玉 皮包差
        System.out.println(s11);//暴雨and 暴雨黛玉 皮包差

        //5.split 分割字符串，对于某些分割字符，我们需要 转义比如
         //老韩解读： 以，为标准对poem进行分割，返回一个数组
  String poem = "锄禾日当午,汗滴禾下土,谁知盘中餐,粒粒皆辛苦";
       //对字符串精心分割时加入转义符“\”
  String [] split = poem.split(",");
        poem = "E:\\aaa\\bbb";//"\"是转义符
        split = poem.split("\\\\");


  System.out.println("===分割后内容====");
        for (int i = 0; i < split.length; i++) {
            System.out.println(split[i]);
        }结果：

锄禾日当午
汗滴禾下土
谁知盘中餐
粒粒皆辛苦

       s="happy";
        char[]chs = s.toCharArray();
        for (int i = 0; i < chs.length; i++) {
            System.out.println(chs[i]);}
            //7.compareTo 比较两个字符串的大小，如果前者大，
            //则返回正数，后者大，则返回负数，如果相等，返回0
            //如果长度相同，并且每个自负也相同，就返回0
            //如果长度相同或者不相同，但是在进行比较时，可以区分大小
            //就返回c1-c2
            //如果前面的部分都相同，就返回str1.len - str2.len

            String a ="jackkkl";//len = 7
            String b ="jack";// len = 4
            System.out.println(a.compareTo(b));//返回值就是‘c' - 'a' = 3 的值
            //8.format格式字符串
            /*format//格式字符串，%s字符串%c字符%d整型%2f浮点型
             * 案例，将一个人的信息格式化输出

             */
            String name1 ="jack";
            int age = 9;
            int score = 99;
            char gender = '男';
             String formatStr ="我的名字是%s 年龄是%d,成绩%d 性别是%c,希望大家喜欢我";
             String info2 = String.format(formatStr,name1,age,score,gender);
            System.out.println(info2);
 //称为：%s字符串类型，%c字符型，%b布尔类型，%d整数类型，%.2f float类型
        //这些占位符由后面变量来替换
        //%s表示后面由 字符串来替换
        //%d是整数来替换
        //%.2f是double类型
    }
}

========================================
输出结果：
Success!
3
0
张三
llo
2
HELLO
hello
helloddsfffpp
暴雨and 林黛玉 皮包差
暴雨and 暴雨黛玉 皮包差
===分割后内容====
E:
aaa
bbb
h
a
p
p
y
3
我的名字是jack 年龄是9,成绩11.00 性别是男,希望大家喜欢我

ckage com.hspedu.wrapper;

/**
 * @author 郑道炫
 * @version 1.0
 */
public class Homework03 {



    public static void main(String[] args) {
        /**
         * Han shun Ping的人名，以Ping,han .S形式
         * 用分割split（“ ”）
         * 对得到的String【】进行格式化 String.format
         */
        String dd="Han shun Ping";



        String ss=" ";
        String[]ne =dd.split(ss);


        for (int i = 0; i < ne.length; i++) {
            System.out.println(ne[i]);
        }
        System.out.println("============改之前==================");

        String num1 = ne[0];
       String num2 = ne[1].substring(0,1).toUpperCase();
        String num3 = ne[2];
        String formatStr ="%s,%s.%s";
        String info = String.format(formatStr,num3,num1,num2);



       System.out.println(info);



        System.out.println("========我自己做的==============");
        System.out.println("======正确答案==========");

       String names = "Han shun Ping";
       function(names);

    }
    public static void function(String sa){
        if (sa == null) {
            System.out.println("sa 不能为空");
              return;}
         String[] names = sa.split(" ");
        if (names.length != 3){
            System.out.println("输入的字符串格式不对");
            return;
        }
       String mm = String.format("%s,%s.%c",names[2],names[0],names[1].toUpperCase().charAt(0));
        System.out.println(mm);
    }
}


---
layout:     post
title:      JDKAPI(System;Integer;Math)
subtitle:   
date:       2019-09-07
author:     Mehaei
header-img: img/post-bg-keybord.jpg
catalog: true
tags:
    - python
---
# <a id="JDK_API_0"></a>JDK API

[JDK API官网](https://docs.oracle.com/javase/8/docs/api/)

## <a id="_System_3"></a>一. System类

#### <a id="1_4"></a>1.用途

Among the facilities provided by the System class are standard input, standard output, and error output streams; access to externally defined properties and environment variables; a means of loading files and libraries; and a utility method for quickly copying a portion of an array.<br>
即System类提供的功能包括标准输入，标准输出和错误输出流; 访问外部定义的属性和环境变量; 加载文件和库的方法; 以及用于快速复制阵列的一部分的实用方法

#### <a id="2_7"></a>2.特点

It cannot be instantiated.即不能被实例化

#### <a id="3_9"></a>3.基本字段

<img src="https://img-blog.csdnimg.cn/20190907155800843.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjYxNTU4,size_16,color_FFFFFF,t_70" alt="官方文档中System基本字段">

#### <a id="4_11"></a>4.所有方法

<img src="https://img-blog.csdnimg.cn/20190907160141658.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjYxNTU4,size_16,color_FFFFFF,t_70" alt="官方文档System所有方法">

#### <a id="5_13"></a>5.常用方法

Field Detail

<li>in<br>
  “标准”输入流。此流已打开并准备好提供输入数据。通常，该流对应于键盘输入或由主机环境或用户指定的另一输入源。</li>

read<br>
  从输入流中读取下一个数据字节。值字节作为int返回，范围为0到255。如果没有字节可用，因为已到达流的末尾，则返回值-1。此方法将阻塞，直到输入数据可用，检测到流的末尾或抛出异常。子类必须提供此方法的实现。

<li>out<br>
 “标准”输出流。此流已打开并准备接受输出数据。通常，该流对应于主机环境或用户指定的显示输出或另一输出目的地。</li>

对于简单的独立Java应用程序，编写一行输出数据的典型方法是：

```
<code>System.out.println(data)
</code>
```

1<br>
（1）println<br>
换行输出。<br>
参数可以接受：无参数、char、int、long、float、double、char[]、String、Object。

（2）append<br>
将指定的字符、字符序列追加到此输出流。

```
<code>import java.io.IOException;
public class intest {
	public static void main(String[] args) throws IOException {
				char c = 'p';
				System.out.print("888");
				System.out.append(c);
	}
}
</code>
```

输出

```
<code>888p
</code>
```

（3）print<br>
不换行输出。<br>
可以接受的参数：boolean、char、int、long、float、double、char[]、String、Object。

<li>err<br>
  “标准”错误输出流。此流已打开并准备接受输出数据。<br>
  通常，该流对应于主机环境或用户指定的显示输出或另一输出目的地。按照惯例，此输出流用于显示应立即引起用户注意的错误消息或其他信息，即使主要输出流（变量out的值）已重定向到文件或其他目标，即通常不会持续监控。</li>
<li>exit<br>
  终止当前运行的Java虚拟机。该参数用作状态代码；按照惯例，非零状态代码表示异常终止。</li>

此方法在类Runtime中调用exit方法。此方法永远不会正常返回。

调用System.exit(n)实际上等同于调用：

```
<code>Runtime.getRuntime().exit(n)
</code>
```

## <a id="_Integer_67"></a>二. Integer类

#### <a id="1_68"></a>1.用途

The Integer class wraps a value of the primitive type int in an object. An object of type Integer contains a single field whose type is int.<br>
In addition, this class provides several methods for converting an int to a String and a String to an int, as well as other constants and methods useful when dealing with an int.<br>
Integer类在对象中包装基本类型int的值。 Integer类型的对象包含一个类型为int的字段。<br>
此外，这个类提供了几种方法，用于将int转换为String，将String转换为int，以及在处理int时有用的其他常量和方法。

#### <a id="2_73"></a>2.特点

int的包装类

#### <a id="3_75"></a>3.基本字段

<img src="https://img-blog.csdnimg.cn/20190907162356602.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjYxNTU4,size_16,color_FFFFFF,t_70" alt="Integer字段">

#### <a id="4_77"></a>4.所有方法

<img src="https://img-blog.csdnimg.cn/20190907162505944.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjYxNTU4,size_16,color_FFFFFF,t_70" alt="Integer方法">

#### <a id="5_79"></a>5.常用方法

<li>toString<br>
  把int转String</li>

```
<code>    //方法一:Integer类的静态方法toString()
    Integer a = 2;
    String str = Integer.toString(a)
     
    //方法二:Integer类的成员方法toString()
    Integer a = 2;
    String str = a.toString();
     
    //方法三:String类的静态方法valueOf()
    Integer a = 2;
    String str = String.valueOf(a);
</code>
```

<li>parseInt<br>
  把String转int</li>

```
<code>     Integer.parseInt("10");			//返回 整型10
</code>
```

1. valueOf

```
<code>     `String s = "123";
    Integer num = Integer.valueOf(s);		//返回 整型123
</code>
```

<li>compare(x,y)<br>
  如果x==y，返回0；<br>
  如果x>y，返回一个大于0的数；<br>
  如果x<y，返回一个小于0的数。</li>
<li>reverse<br>
  二进制按位反转。</li>
<li>reverseByte<br>
  二进制按byte反转。</li>
<li>signum<br>
  返回指定int值的signum函数。（如果指定的值为负，则返回值为-1;如果指定的值为零，则返回0;如果指定的值为正，则返回1。）</li>
<li>sum(a,b)<br>
  返回a+b。</li>
<li>max(a,b)<br>
  取a和b中的较大值。</li>
<li>min(a,b)<br>
  取a和b中的较小值。</li>

## <a id="_Math_123"></a>三. Math类

#### <a id="1_124"></a>1.用途

Math类包含执行基本数值运算的方法，例如基本指数，对数，平方根和三角函数。

#### <a id="2_126"></a>2.特点

Unlike some of the numeric methods of class StrictMath, all implementations of the equivalent functions of class Math are not defined to return the bit-for-bit same results. This relaxation permits better-performing implementations where strict reproducibility is not required.<br>
即与StrictMath类的某些数值方法不同，类Math的等效函数的所有实现都未定义为返回逐位相同的结果。这种放松允许在不需要严格再现性的情况下实现性能更好的实施。

#### <a id="3_129"></a>3.基本字段

<img src="https://img-blog.csdnimg.cn/20190907162753440.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjYxNTU4,size_16,color_FFFFFF,t_70" alt="Math字段">

#### <a id="4_131"></a>4.所有方法

<img src="https://img-blog.csdnimg.cn/20190907162837204.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjYxNTU4,size_16,color_FFFFFF,t_70" alt="Math方法">

#### <a id="5_134"></a>5.常用方法

<li>E<br>
  双重值比其他任何一个都更接近e，即自然对数的基数。</li>
<li>PI<br>
  比pi更接近pi的双值，即圆周长与直径的比值。</li>
<li>sin<br>
  返回角度的三角正弦值。<br>
Parameters:<br>
a - 以弧度表示的角度。</li>
<li>cos<br>
  返回角度的三角余弦值。<br>
Parameters:<br>
a - 以弧度表示的角度。</li>
<li>tan<br>
  返回角度的三角正切。<br>
Parameters:<br>
a - 以弧度表示的角度。</li>
<li>asin<br>
返回值的反正弦值;返回的角度在-pi / 2到pi / 2的范围内。<br>
Parameters:<br>
a - 返回其正弦值的值。</li>
<li>acos<br>
返回值的反余弦值;返回的角度在0.0到pi的范围内。<br>
Parameters:<br>
a - 返回其余弦值的值。</li>
<li>atan<br>
返回值的反正切;返回的角度在-pi / 2到pi / 2的范围内。<br>
Parameters:<br>
a - 返回反正切的值。</li>
<li>toRadians<br>
将以度为单位的角度转换为以弧度为单位测量的近似等效角度。从度到弧度的转换通常是不精确的。<br>
Parameters:<br>
angdeg - 一个角度，以度为单位</li>
<li>toDegrees<br>
将以弧度测量的角度转换为以度为单位测量的近似等效角度。从弧度到度数的转换通常是不精确的;用户不应期望cos（toRadians（90.0））完全等于0.0。<br>
Parameters:<br>
angdeg - 一个角度，以度为单位</li>
<li>exp<br>
指数。<br>
参数：<br>
a - 将e提升到的指数。</li>
<li>log<br>
以e为底的对数。</li>
<li>log10<br>
以10为底的对数。</li>
<li>sqrt<br>
开方。</li>
<li>cbrt<br>
开立方。</li>
<li>ceil<br>
向上取整。</li>
<li>floor<br>
向下取整。</li>
<li>round<br>
四舍五入。</li>
<li>pow(a,b)<br>
a的b次方</li>
<li>random<br>
返回带有正号的double值，大于或等于0.0且小于1.0。返回值是伪随机选择的，具有来自该范围的（近似）均匀分布。</li>
<li>addExact(a,b)<br>
加法a+b。</li>
<li>subtractExact(a,b)<br>
减法a-b。</li>
<li>multiplyExact(a,b)<br>
乘法a*b。</li>
<li>abs<br>
绝对值。</li>
<li>max<br>
最大值。</li>
<li>min<br>
最小值。</li>

# <a id="_205"></a>总结

#### <a id="_206"></a>学习心得

JDK提供了丰富的类库，JDK官方文档给出了所有的Interfaces、Classes、Enums、Exceptions、Errors、Annotation Types的说明，对于每个类都有字段、方法的说明，是我们学习过程中需要经常查阅的资料，很多方法jdk类库里面都有，不需要我们再去写，比如栈、队列、排序等等，只需调用即可。

###### <a id="_208"></a>附参考博客:

[JDK API（SE8）(部分System，Math，Integer类)](https://blog.csdn.net/Sherry_Yue/article/details/100593849)

---
layout:     post
title:      Java包（package）的实例
subtitle:   
date:       2019-09-22
author:     Mehaei
header-img: img/post-bg-unix-linux.jpg
catalog: true
tags:
    - python
---
## <a id="1__0"></a>1. 首先是没有引入包的源码

```
<code>public class FighterPlane {
	String name;
	int missileNum;
	void fire() {
		if(missileNum > 0) {
			System.out.println("now fire a missile!");
			missileNum -= 1;
		}
		else {
			System.out.println("No missile left!");
			
		}
	}
}

public class RunPlane {
		public static void main(String args[]) {
			FighterPlane fp = new FighterPlane();
			fp.name = "苏35";
			fp.missileNum = 6;
			fp.fire();
		}
}
</code>
```

虽然没有引入包,但这是包的一种特殊存在形式----默认包

## <a id="2__29"></a>2. 引入包

### <a id="1_30"></a>（1）目录形式包

#### <a id="_31"></a>建立如图文件夹

<img src="https://img-blog.csdnimg.cn/20190922162053748.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjYxNTU4,size_16,color_FFFFFF,t_70" alt="建立文件夹"><br>
将FighterPlane.java存在com.resource文件夹中,将RunPlane.java存放到com.run文件夹中,deliver文件夹用于存放包文件.

#### <a id="_34"></a>修改源代码

FighterPlane.java文件：

```
<code>package com.resource;
public class FighterPlane
{
   public String name;
   public int missileNum;
   public void fire(){
       if (missileNum>0){
          System.out.println("now fire a missile !");
		  missileNum -= 1; 
       }
       else{
          System.out.println("No missile left !");
       }
   }   
}


</code>
```

进入4.16目录，执行命令行

```
<code>javac -d .\deliver com\resourde\FighterPlane.java
</code>
```

在deliver文件夹下出现com、resource的子目录，看作包。

RunPlane.java文件：

```
<code>package com.run;
import com.resource.*;
public class RunPlane
{
	public static void main(String args[]){
       FighterPlane fp = new FighterPlane();
	   fp.name = "苏35";
	   fp.missileNum = 6;
	   fp.fire();
   }
};
</code>
```

进入4.16目录，编译，执行命令行

```
<code>javac -d .\deliver -classpath .\deliver com\resourde\RunPlane.java
</code>
```

执行RunPlane.

```
<code>java  -classpath .\deliver com.run.RunPlane
</code>
```

目录形式包创建成功

### <a id="2jar_85"></a>（2）jar文件包

将先前的包通过如下命令压缩成一个文件

```
<code>Jar cvf first.jar -C deliver .
</code>
```

jar为JDK工具，c（create，创建一个新文件）；v（生成详细输出到标准输出上）；f（指定存档文件名，也就是后面的first,jar）;-C的作用是将指定目录下的所有包进行打包；“deliver .”是你将其下所有文件压缩到first.jar当中。

有了first.jar,就可以采用如下方式执行程序，假设当前路径为“D:\”下

```
<code>java -classpath d:\4.16\first.jar com.run.RunPlane
</code>
```

jar包创建成功

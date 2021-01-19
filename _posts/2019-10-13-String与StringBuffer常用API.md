---
layout:     post
title:      String与StringBuffer常用API
subtitle:   
date:       2019-10-13
author:     Mehaei
header-img: img/post-bg-mma-5.jpg
catalog: true
tags:
    - python
---
### <a id="String_0"></a>String

参看 Java String API 文档：[Java String API](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html)

<li>char charAt(int index)<br>
返回指定索引处的 char 值。</li>
<li>int compareTo(Object o)<br>
把这个字符串和另一个对象比较。</li>
<li>int compareTo(String anotherString)<br>
按字典顺序比较两个字符串。</li>
<li>int compareToIgnoreCase(String str)<br>
按字典顺序比较两个字符串，不考虑大小写。</li>
<li>String concat(String str)<br>
将指定字符串连接到此字符串的结尾。</li>
<li>boolean contentEquals(StringBuffer sb)<br>
当且仅当字符串与指定的StringBuffer有相同顺序的字符时候返回真。</li>
<li>static String copyValueOf(char[] data)<br>
返回指定数组中表示该字符序列的 String。</li>
<li>static String copyValueOf(char[] data, int offset, int count)<br>
返回指定数组中表示该字符序列的 String。</li>
<li>boolean endsWith(String suffix)<br>
测试此字符串是否以指定的后缀结束。</li>
<li>boolean equals(Object anObject)<br>
将此字符串与指定的对象比较。</li>
<li>boolean equalsIgnoreCase(String anotherString)<br>
将此 String 与另一个 String 比较，不考虑大小写。</li>
<li>byte[] getBytes()<br>
使用平台的默认字符集将此 String 编码为 byte 序列，并将结果存储到一个新的 byte 数组中。</li>
<li>byte[] getBytes(String charsetName)<br>
使用指定的字符集将此 String 编码为 byte 序列，并将结果存储到一个新的 byte 数组中。</li>
<li>void getChars(int srcBegin, int srcEnd, char[] dst, int dstBegin)<br>
将字符从此字符串复制到目标字符数组。</li>
<li>int hashCode()<br>
返回此字符串的哈希码。</li>
<li>int indexOf(int ch)<br>
返回指定字符在此字符串中第一次出现处的索引。</li>
<li>int indexOf(int ch, int fromIndex)<br>
返回在此字符串中第一次出现指定字符处的索引，从指定的索引开始搜索。</li>
<li>int indexOf(String str)<br>
返回指定子字符串在此字符串中第一次出现处的索引。</li>
<li>int indexOf(String str, int fromIndex)<br>
返回指定子字符串在此字符串中第一次出现处的索引，从指定的索引开始。</li>
<li>String intern()<br>
返回字符串对象的规范化表示形式。</li>
<li>int lastIndexOf(int ch)<br>
返回指定字符在此字符串中最后一次出现处的索引。</li>
<li>int lastIndexOf(int ch, int fromIndex)<br>
返回指定字符在此字符串中最后一次出现处的索引，从指定的索引处开始进行反向搜索。</li>
<li>int lastIndexOf(String str)<br>
返回指定子字符串在此字符串中最右边出现处的索引。</li>
<li>int lastIndexOf(String str, int fromIndex)<br>
返回指定子字符串在此字符串中最后一次出现处的索引，从指定的索引开始反向搜索。</li>
<li>int length()<br>
返回此字符串的长度。</li>
<li>boolean matches(String regex)<br>
告知此字符串是否匹配给定的正则表达式。</li>
<li>boolean regionMatches(boolean ignoreCase, int toffset, String other, int ooffset, int len)<br>
测试两个字符串区域是否相等。</li>
<li>boolean regionMatches(int toffset, String other, int ooffset, int len)<br>
测试两个字符串区域是否相等。</li>
<li>String replace(char oldChar, char newChar)<br>
返回一个新的字符串，它是通过用 newChar 替换此字符串中出现的所有 oldChar 得到的。</li>
<li>String replaceAll(String regex, String replacement)<br>
使用给定的 replacement 替换此字符串所有匹配给定的正则表达式的子字符串。</li>
<li>String replaceFirst(String regex, String replacement)<br>
使用给定的 replacement 替换此字符串匹配给定的正则表达式的第一个子字符串。</li>
<li>String[] split(String regex)<br>
根据给定正则表达式的匹配拆分此字符串。</li>
<li>String[] split(String regex, int limit)<br>
根据匹配给定的正则表达式来拆分此字符串。</li>
<li>boolean startsWith(String prefix)<br>
测试此字符串是否以指定的前缀开始。</li>
<li>boolean startsWith(String prefix, int toffset)<br>
测试此字符串从指定索引开始的子字符串是否以指定前缀开始。</li>
<li>CharSequence subSequence(int beginIndex, int endIndex)<br>
返回一个新的字符序列，它是此序列的一个子序列。</li>
<li>String substring(int beginIndex)<br>
返回一个新的字符串，它是此字符串的一个子字符串。</li>
<li>String substring(int beginIndex, int endIndex)<br>
返回一个新字符串，它是此字符串的一个子字符串。</li>
<li>char[] toCharArray()<br>
将此字符串转换为一个新的字符数组。</li>
<li>String toLowerCase()<br>
使用默认语言环境的规则将此 String 中的所有字符都转换为小写。</li>
<li>String toLowerCase(Locale locale)<br>
使用给定 Locale 的规则将此 String 中的所有字符都转换为小写。</li>
<li>String toString()<br>
返回此对象本身（它已经是一个字符串！）。</li>
<li>String toUpperCase()<br>
使用默认语言环境的规则将此 String 中的所有字符都转换为大写。</li>
<li>String toUpperCase(Locale locale)<br>
使用给定 Locale 的规则将此 String 中的所有字符都转换为大写。</li>
<li>String trim()<br>
返回字符串的副本，忽略前导空白和尾部空白。</li>
<li>static String valueOf(primitive data type x)<br>
返回给定data type类型x参数的字符串表示形式。</li>

### <a id="StringBuffer_94"></a>StringBuffer

参看 Java StringBuffer API 文档：[Java StringBuffer API](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuffer.html)<br>
主要方法：

<li>public StringBuffer append(String s)<br>
将指定的字符串追加到此字符序列。</li>
<li>public StringBuffer reverse()<br>
将此字符序列用其反转形式取代。</li>
<li>public delete(int start, int end)<br>
移除此序列的子字符串中的字符。</li>
<li>public insert(int offset, int i)<br>
将 int 参数的字符串表示形式插入此序列中。</li>
<li>replace(int start, int end, String str)<br>
使用给定 String 中的字符替换此序列的子字符串中的字符。</li>

下面方法和 String 类的方法类似：

<li>int capacity()<br>
返回当前容量。</li>
<li>char charAt(int index)<br>
返回此序列中指定索引处的 char 值。</li>
<li>void ensureCapacity(int minimumCapacity)<br>
确保容量至少等于指定的最小值。</li>
<li>void getChars(int srcBegin, int srcEnd, char[] dst, int dstBegin)<br>
将字符从此序列复制到目标字符数组 dst。</li>
<li>int indexOf(String str)<br>
返回第一次出现的指定子字符串在该字符串中的索引。</li>
<li>int indexOf(String str, int fromIndex)<br>
从指定的索引处开始，返回第一次出现的指定子字符串在该字符串中的索引。</li>
<li>int lastIndexOf(String str)<br>
返回最右边出现的指定子字符串在此字符串中的索引。</li>
<li>int lastIndexOf(String str, int fromIndex)<br>
返回 String 对象中子字符串最后出现的位置。</li>
<li>int length()<br>
返回长度（字符数）。</li>
<li>void setCharAt(int index, char ch)<br>
将给定索引处的字符设置为 ch。</li>
<li>void setLength(int newLength)<br>
设置字符序列的长度。</li>
<li>CharSequence subSequence(int start, int end)<br>
返回一个新的字符序列，该字符序列是此序列的子序列。</li>
<li>String substring(int start)<br>
返回一个新的 String，它包含此字符序列当前所包含的字符子序列。</li>
<li>String substring(int start, int end)<br>
返回一个新的 String，它包含此序列当前所包含的字符子序列。</li>
<li>String toString()<br>
返回此序列中数据的字符串表示形式。</li>

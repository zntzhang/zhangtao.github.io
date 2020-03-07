---
layout:  post
title:   Integer比较 ==与equals
date:   2020-03-06 15:52
author:  "张涛"
header-img: "img/post-bg-2015.jpg"
catalog:   false
tags:
    - java
---

    class Test {
    
        public static void main(String[] args) {
    
            Integer i1 = new Integer(5);
    
            Integer i2 = new Integer(5);
    
            System.out.println(i1 == i2); //false (情况，即new的id，而不是=的id赋值)
    
    
    
            Integer i3 = 5;
    
            Integer i4 = 5;
    
            System.out.println(i3 == i4); //true
    
        }
    
    }

所以判断Integer相等的值最好不要用==

下面为更为详细的解析：

    
    
    public static void main(String[] args) {  
            Integer a1 = Integer.valueOf(60);  //danielinbiti  
            Integer b1 = 60;    
            System.out.println("1:="+(a1 == b1));     
    
    
            Integer a2 = 60;    
            Integer b2 = 60;    
            System.out.println("2:="+(a2 == b2));    
    
    
            Integer a3 = new Integer(60);    
            Integer b3 = 60;    
            System.out.println("3:="+(a3 == b3));    
    
            Integer a4 = 129;    
            Integer b4 = 129;    
            System.out.println("4:="+(a4 == b4));    
        }  

上述代码的答案，涉及到Java缓冲区和堆的问题。

Integer b3=60,这是一个装箱过程也就是Integer b3=Integer.valueOf(60)  
而查看Integer拆装箱的源码会发现  
（ **Integer在拆装箱时会调用 IntegerCache** ）

    
    
    public static Integer valueOf(String s) throws NumberFormatException {
            return Integer.valueOf(parseInt(s, 10));
        }
    
    public static Integer valueOf(int i) {
            if (i >= IntegerCache.low && i <= IntegerCache.high)
                return IntegerCache.cache[i + (-IntegerCache.low)];
            return new Integer(i);
        }

java中 **Integer类型对于-128-127之间的数是缓冲区取的** ，所以用等号比较是一致的。
**但对于不在这区间的数字是在堆中new出来的** 。所以地址空间不一样，也就不相等。  
ps.两个new的Integer永远不相等

所以，以后碰到Integer比较值是否相等需要用intValue()

对于Double没有缓冲区。

答案

1:=true

2:=true

3:=false

4:=false

##  结论

  1. Integer类型的数据在 ` -128~127 ` 范围内用 ` ==和equals比较的结果是一样 ` 的，超出此范围才会出现差异。 
  2. java中Integer类型对于-128-127之间的数是缓冲区取的，所以用等号比较是一致的。 
  3. 但对于不在这区间的数字是在堆中 ` new出来 ` 的。所以 ` 地址空间不一样，也就不相等 ` 。 


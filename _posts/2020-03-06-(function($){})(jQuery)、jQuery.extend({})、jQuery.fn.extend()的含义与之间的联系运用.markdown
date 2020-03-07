---
layout:  post
title:   (function($){})(jQuery)、jQuery.extend({})、jQuery.fn.extend()的含义与之间的联系运用
date:   2020-03-06 15:52
author:  "唐传林"
header-img: "img/post-bg-2015.jpg"
catalog:   false
tags:

---
##  1\. (function($){})(jQuery)的含义

  * 首先讲(function(){})();的含义，它是一个 **立即执行函数** ；相当于先申明一个函数，声明完后直接调用；   
e.g ` (function(str){alert(str)})("output")); `  
相当于：  
` function OutPutFun(str){alert(str);}; `  
` OutPutFun("output"); `

  * (function($) {…})(jQuery)的含义   
相当于  
` function aa($){}; `  
`  
aa(jQuery) `  
页面加载完把jquery对象传给匿名函数,并且用$作为形参,在函数的具体逻辑中调用

##  2\. jQuery.extend({})的含义

我们先把jQuery看成了一个类，这样好理解一些。jQuery.extend()，就是给jQuery这个类添加静态方法。  
e.g  
通过jQuery.extend({})添加check()后,可以通过$.check()调用

##  3\. jQuery.fn.extend()的含义

jQuery.fn.extend,就是给jQuery对象( 例如 ` $("#abc") ` )添加方法(即实例方法)  
  
e.g  
通过jQuery.fn.extend()添加check()后,可以通过 ` $("#id").check() ` 调用

##  4\. extend方法原型

var dest1 = extend(dest,src1,src2,src3…);  
它的含义是将src1,src2,src3…合并到dest中,返回值为合并后的dest

##  5\. (function($){})(jQuery)与jQuery.extend({})两者一起使用的情况

` (function($){ `  
  
` $.extend({ ` **//2.调用jQuery.extend({}),给jquery类添加websocketSettings方法**  
  
` speak:function(){ `  
  
` alert("how are you!"); `  
  
}  
  
` }); `  
` })(jQuery); ` // **1.页面加载调用,把jquery对象传入,赋值给$**  
  
**3.可以通过$.speak()调用方法**


<!--
 * @Author: cocoon
 * @Date: 2020-10-01 13:28:01
 * @LastEditTime: 2020-10-03 23:11:18
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: /Frontend-02-Template/week02/NOTE.md
-->

# 前端训练营-week02 丨 重学JavaScript

## 预习内容

第 2、3 周预习知识点：

- [JavaScript 类型：关于类型，有哪些你不知道的细节？](https://time.geekbang.org/column/article/78884 "JavaScript 类型：关于类型，有哪些你不知道的细节？")
- [JavaScript 对象：面向对象还是基于对象？](https://time.geekbang.org/column/article/79319 "JavaScript 对象：面向对象还是基于对象？")
- [JavaScript 对象：我们真的需要模拟类吗？](https://time.geekbang.org/column/article/79539 "JavaScript 对象：我们真的需要模拟类吗？")
- [JavaScript 对象：你知道全部的对象分类吗？](https://time.geekbang.org/column/Article/80011 "JavaScript 对象：你知道全部的对象分类吗？")
- [JavaScript 执行（一）：Promise 里的代码为什么比 setTimeout 先执行？](https://time.geekbang.org/column/article/82764 "JavaScript 执行（一）：Promise 里的代码为什么比 setTimeout 先执行？")
- [JavaScript 执行（二）：闭包和执行上下文到底是怎么回事？](https://time.geekbang.org/column/article/83302 "JavaScript 执行（二）：闭包和执行上下文到底是怎么回事？")
- [JavaScript 执行（三）：你知道现在有多少种函数吗？](https://time.geekbang.org/column/article/83719 "JavaScript 执行（三）：你知道现在有多少种函数吗？")
- [JavaScript 执行（四）：try 里面放 return，finally 还会执行吗？](https://time.geekbang.org/column/article/83860 "JavaScript 执行（四）：try 里面放 return，finally 还会执行吗？")
- [JavaScript 词法：为什么 12.toString 会报错？](https://time.geekbang.org/column/article/86400 "JavaScript 词法：为什么 12.toString 会报错？")
- [（小实验）理解编译原理：一个四则运算的解释器](https://time.geekbang.org/column/article/86823 "（小实验）理解编译原理：一个四则运算的解释器")
- [JavaScript 语法（预备篇）：到底要不要写分号呢？](https://time.geekbang.org/column/article/87179 "JavaScript 语法（预备篇）：到底要不要写分号呢？")
- [JavaScript 语法（一）：在 script 标签写 export 为什么会抛错？](https://time.geekbang.org/column/article/87808 "JavaScript 语法（一）：在 script 标签写 export 为什么会抛错？")
- [JavaScript 语法（二）：你知道哪些 JavaScript 语句？](https://time.geekbang.org/column/article/88538 "JavaScript 语法（二）：你知道哪些 JavaScript 语句？")
- [JavaScript 语法（三）：什么是表达式语句？](https://time.geekbang.org/column/article/88827 "JavaScript 语法（三）：什么是表达式语句？")
- [JavaScript 语法（四）：新加入的 ** 运算符，哪里有些不一样呢？](https://time.geekbang.org/column/article/89151 "JavaScript 语法（四）：新加入的 ** 运算符，哪里有些不一样呢？")

## 课件

### 录播 | 一、 JS语言通识 | 泛用语言分类方法

#### 1. 语言按语法分类

- 非形式语言
  语法比较自由，没有严格定义
  - 中文
  - 英文等
  
- 形式语言
  具有形式化定义的特点，严谨严格。而在形式语言中还有进一步的分类，下列介绍的分类为乔姆斯基谱系。4种文法是一种上下包含的关系。比如：1型一定属于0型，但是0型不一定属于1型。
  
  - 0型 无限制文法
    定义语言是什么样就是什么样
  - 1型 上下文相关文法
    同样的词句的组合是跟上下文内容相关的
  - 2型 上下文无关文法
    同样一个表达，不管放在哪里，都是一样的意思
  - 3型 正则文法
    能够被正则表达式去描述的一种文法

  产生式这一工具可以让大家能够严格地去描述乔姆斯基谱系里面的各种文法。

### 录播 | 二、 JS语言通识 | 什么是产生式

#### 1. 产生式（BNF）

产生式：巴科斯-诺尔范式 (BNF)

实际上产生式有多种。不同文档会选用不同的产生式的方式，但是他们的大体结构和表达的能力相近​。巴科斯-诺尔范式，属于其中最经典也是最常用的一种描述方法。

- < > 用尖括号括起来的名称来表示语法结构名，如中文里有主谓宾，编程语言里的if语句、函数都是类似的描述它的语法语句
- 语法结构分成基础结构和需要用其他语法结构定义的复合结构
  - 基础结构称终结符（Terminal Symbol）
  - 复合结构称非终结符（Nonterminal Symbol）
  语言里一定有很多终结符，然后由这些终结符形成一定语法结构，来产生一些非终结符。一般我们语言中都有一个最上层的非终结符来代表整个语言的文体。

- " " 引号和中间的字符表示终结符，即用字符串来表示终结符
- （）可以有括号，以此产生不同的结构。用括号括起来变成一组
- \* 表示可以重复多次
- | 表示或，竖线两边的是可选内容
- \+ 表示至少一次

比如说要做一个字母a的列表，则就会把字母a用双引号引起来，而列表如果说这个列表里的a至少要出现一次，那么则会在a后面加上一个加号 `a+`。而如果想做一个a或者b字母的列表则会写 `a|b`然后外面阔起来再加上加号 `(a|b)+`。这就是我们产生式的一个基本写法。  

实例  定义四则运算：  

``` html
<MultiplicativeExpression>::=<Number>|
        <MultiplicativeExpression>"*"<Number>|
        <MultiplicativeExpression>"/"<Number>|
<AddtiveExpression>::=<Number>|
        <AddtiveExpression>"+"<MultiplicativeExpression>|
        <AddtiveExpression>"-"<MultiplicativeExpression>|
```

1 + 2 * 3

由左边的 1 加上 右边 2 \* 3 的结果组成的语法结构，2 \* 3 是一个子结构，而 2 \* 3 中包含左右的 numbner 和 运算符 * 。

终结符：
Number
\+ - * /
非终结符：
MultiplicativeExpression （乘法的结构）
AddtiveExpression （加法的结构）
BNF
常用BMF使用技巧
将特殊的number定义为一个乘法结构，此时定义加法的时候可以认为左右都是一个乘法结构

>先定义一个加法表达式，让它等于一个乘法表达式的列表。那么这个BNF的定义是可以递归的，则可定义它要么是一个单独的乘法表达式，要么是一个加法表达式加上或者减去一个乘法的表达式。这样就能得到一个这样的加法的定义。乘法的表达式也类似,只不过是我们把乘法表达式的位置换成Number就可以了。这里面我们可以发现所有的终结符就包括 Number、加、减、乘、除 这些都属于终结符。而非终结符就是 MultiplicativeExpressio 和 AddtiveExpression 。注意到这里有把一个单独的 Number 也定义为了一种特殊的乘法的结构，这样就可以在定义加法的时候比较简单。即可以认为这个左右都是一个乘法结构。这是一个比较常用的使用BNF的小技巧。这样就描述出来了四则运算。  

### 录播 | 三、 JS语言通识 | 深入理解产生式

#### 1. 通过产生式理解乔姆斯基谱系

- 0型 无限制文法  
  - `?::=?`
  一个短短的 A 就可以产生10个不同的非终结符，然后由他们再组成一些复杂的这样的语法结构。所以无限制文法中可以随便写，定义的左边和右边，写什么都可以
  
- 1型 上下文相关文法
  - `?<A>?::=?<B>?`
  虽然可以左右两边都写多个非终结符。但是会发现虽然可以写多个，但变的只能是有一个。那么左边变化的只能有一个，而变的部分一定是有一个前面和后面，这样的一个关系，一定是有一个固定不变的部分。即前面蓝色问号 `？` 开头的部分和后面橙色问号 `？` 结束的部分。即蓝色问号的部分叫做上文，橙色问号的部分就叫做下文。所以上下文相关文法它就是一个根据前后来判别每一个符号，它所表达的意义的这样一种文法

- 2型 上下文无关文法
  - `<A>::=?`
  左边只能有一个非终结符，而右边可以随便写。可以是一大堆终结符，也可以是终结符和非终结符的混合。
- 3型 正则文法
  - `<A>:=<A>?`
  - `<A>:=?<A>` ❌
  正则文法假如是递归定义的。那么它不允许你这个定义A出现在尾巴上。比如说左边是一个符号A，那么右边A一定是出现在产生式的最开头。一定不能出现在结尾。根据这个规则，所有的正则文法都是可以用正则表达式来表示的。  
  
>提问：JavaScript是上下文相关文法还是上下文无关文法，以及JavaScript是否是正则文法？

JavaScript虽然总体上属于上下文无关文法，其中的表达式部分大部分属于正则文法。但还有两个特例 ——

``` JavaScript
2 ** 1 ** 2
```

JavaScript表达式里有新加了一个星星运算符 `**` ，表示乘方。乘方运算符其实它就是一个右结合的。所以`2 ** 1 ** 2` 的答案是2。`1**2` 先运算，1的平方仍然是1，2的1次方是2。因为它是右结合的所以不是正则文法，如果再加上if之类语句，就更不是正则文法了。

``` JavaScript
{
  get a {return 1}
  get: 1
}
```

JavaScript也不是一个严格意义上的上下文无关文法。特例比如get，可以理解为类似于关键字，在定义对象的时候，如果在get后面写a，和get后面不写a，它表示的意思是不一样的。写a时它是类似关键字的东西，如果在get后面直接冒号则它自己是属性名。所以这里如果严格按照乔姆斯基谱系来理解，JavaScript其实它属于上下文相关文法。乔姆斯基谱系是一个非常学术的定义方式，在JavaScript引擎的实现上可以理解它总体的编程的结构都是一个针对上下文无关文法的这样的一个分析。而一旦遇到get这样上下文相关文法的地方，那么就会单独用代码做一些特例处理。所以一般来说也不会把JavaScript归结为上下文相关文法去处理，只要有一个特例就会把它变成一个更泛的特例。这就是如何从产生式的角度去理解乔姆斯基谱系。

#### 2. 其他产生式

除了乔姆斯基谱系可以用BNF来定义，其实还有很多不同的产生式的类型。比如后来出现的EBNF、ABNF都是针对BNF做了一些语法上的扩展。不过其实最常见的，一般来说还是每个语言的标准里面都会自己定义一个产生式的书写方法。

``` javascript产生式
AddtiveExpression:
    MultiplicativeExpression
    AddtiveExpression +
MultiplicativeExpression
    AddtiveExpression -
MultiplicativeExpression
```

比如以上就是JavaScript标准里面书写产生式的例子。它开头是缩进来表示的，它的开头相当于产生式左边的非终结符。非终结符后面跟了一个冒号`:`，而之后给了两格缩进。JavaScript产生式的书写方式，它非终结符加号减号是用加粗的黑体字来表示它是终结符的。所以网络上可以看到的产生式五花八门，只学一个BNF是没有办法读懂所有的语言的。但尽管它们有不同的书写方法，但它们所表达的意思都是一样的。理解了产生式背后的思路和原理就可以忽略这种表达方式上的区别。

### 录播 | 四、 JS语言通识 | 现代语言的分类

#### 1. 现代语言的特例

形式语言分类
用途
数据描述语言
JSON、HTML、XAML、SQL、CSS
编程语言
C++、C、Java、C#、Python、Ruby、Perl、Lisp、T-SQL、Clojure、Haskel、JavaScript
表达方式
声明式语言
JSON 、HTML、XAML、SQL、CSS 、Lisp、Clojure、Haskel
命令型语言
C++、C、Java、C#、Python、Ruby、Perl、T-SQL、JavaScript 
类型检查发生时机
静态类型
C、C++,JAVA,C#、go
动态类型
ruby，Python， JavaScript，VBScript，php
类型检查严格程度
强类型
java, C, C++, Python,C#
弱类型
PHP、JavaScript、ASP、Ruby、SQL、VBScript

## 本周作业
四则运算产生式允许带括号，这是应该如何修改产生式

## 本周总结

# 学习总结

……很好，我大概已经预见到后面某拖延症患者的自（补）救（课）生涯了。。

第一周的作业其实是挺不满意的……毕竟梳理整理一类算是自己的长处，老师当时布置的作业内容也是自己曾经颅内思考过的东西。但介于刚搬家的缘故，所以第一周也就那样了吧。毕竟，时间上的问题，有时候确实没办法。只能思考怎么压缩时间，相信时间挤一挤就有了这种真理……

而第二周的课程里最开始的编译原理就难到我了，没有这方面基础，第一课就挺晦涩的。比较好的是，大群并不是僵尸群，有遇到问题提问的人，有独立思考的，有主动分享例子的小伙伴。之前会想助教是否只负责回答主动询问的那种答疑，看到群中这一周的状况，大概要调整的第一个习惯就是，学会如何提问。

这个嘛，下周努力。这一周，我在编译原理起点站这一处卡了太久了。= =

而后面其他的课程内容虽然视频在前几天就都看完了。不理解的地方也有很多，需要多次观看。当前比较愁的问题，大概就是不单是编译原理这种基础知识我不具备，JS方面代码编写我也挺差的……诶，所以做作业方面、理解课程内容时间问题上，我都必须去调整。得让自己跟上课程啊……

[课堂笔记_前端进阶训练营-week02](https://share.mubu.com/doc/47qUcutpWJC "课堂笔记_前端进阶训练营-week02")

---- 20201003 ----
用了mac对新电脑以后重新调整相对满意的写 mark的配置又花了一些额外的时间。但是，有些插件真的装上了就是超级的痛快。13.3的小屏幕实在不适合分栏，mac上的vscode也不知道为何不能直接跨屏，倒腾了插件以后终于在浏览器里直接实时预览笔记效果，弄好后感觉太快乐。咳咳咳，也是为了后面的学习便利嗯！

- [编程范式01范式](https://www.bilibili.com/video/BV1Us411h7aU/?spm_id_from=333.788.videocard.4 "什么是范式")
- [编程范式02BNF](https://www.bilibili.com/video/BV1Us411h72K?from=search&seid=17926377654336906453 "BNF")

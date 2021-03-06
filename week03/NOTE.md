# 前端训练营-week03 丨 重学JavaScript

## 预习内容

- [预习部分见week02](./../week02/NOTE.md)

## 课件

### 录播 | 一、 JS表达式 | 运算符和表达式

<!-- #### JavaScript -->
> JavaScript 语言如何从最小的单位，逐渐构造成一个完整的语言。
> 语法树和运算符优先级的关系，以及运算符左值和右值的区别，类型转换和引用类型。

#### 1. Atom

##### 1.1 Grammar 二叉树

- Grammar Tree vs Priority  语法树与优先级的关系
  - 加减　+-
  - 乘除　*/
  - 括号　()

优先级： () > */ > +-  
乘除会优先形成更小一级的语法结构，而加减会形成更高一级的语法结构。如 1+2*3 会形成下图中的结构。  
2*3 为子树，1加上这一子树会看到如下语法结构（下图为中缀树）。

``` 中缀树
   +
  / \
   1   *
    / \
   2   3
```

运算符的优先级会影响到语法树的构成。所以会发现在JavaScript中它是用产生式来描述运算符的优先级的。  

#### 2.Expression

##### 2.1 Member 运算

- 成员访问 `a.b`
  - -- b 非字符串
- 成员访问 `a[b]`
  - -- [ ]中的b，可以支持运行时的字符串，如果换一个静态语言就不会允许传一个变量在b的这个位置
- foo \`string\`
  - -- 反引号的字符串前面加函数名，会把反引号的字符串部分拆开，然后传进这个函数当作参数，该运算与Member属于同一级，`<u>`实际与Member运算没有关系</u>。
- `super.b`
  - -- 使用super关键字，是只有在我们class的构造函数里面可以用，super关键字 优先级同变量点，变量方括号。
- `super['b']`
- `new.target`
  - -- 两个字都是固定的。 该用法同Member运算优先级。
- `new Foo()`
  - -- 该new优先级同上述。  

##### 2.2 New

- `new Foo`
  - -- 被单独设为一个优先级，被称为 New Expression(new表达式)。  

　关于单独设计 New Expression 的原因在于一个case，见以下实例：  

<!-- TO DO 未理解 Emmm -->
___Example___

- `new a()()`
  - -- 这时 a 后面第一个()，是一个函数调用还是一个new运算的结果呢？此时由于new()结构的优先级更高，所以第一个()是跟着前面new运算的。
- `new new a()`
  - -- 这时的()到底是跟着第一个new还是第二个new呢？因为带()的new它的运算优先级更高，所以它的括号会和第二个new优先级结合。

##### 2.3 Reference 运行时

　关于运行时的设施。a.b 中访问了一个属性，但是其从属性中取出来的并不是属性的值，而是一个引用。
　引用类型是一个确实存在于运行时中的一个JavaScript类型，属于标准中的类型。 一个Reference分为 对象 和 key 两个部分。

- Object
- Key
  - -- key可以是 String 也可以是 Symbol  

　delete 和 assign 就是用到的reference类型。当做加减法运算时就会把 reference 直接解引用，像普通的变量一样去使用。  
　当把Member运算或者assign放在一个等号的左边， 同样要知道把右边的这个表达式赋值给哪一个对象的哪一个属性。这就是引用类型的一个关键特征。  
　JavaScript语言就是引用类型在运行时来处理删除或者赋值这样的相关操作的。

- delete
- assign

##### 2.4 Call 函数调用

> Call Expression 是一个统称。 最基础的Call Expression 就是一个函数后边跟了一对圆括号。其优先级低于new，同时低于前面所有Member运算。但是在括号之后加上取属性，则会让表达式降级为Call Expression。
> 语法结构能够表达的是要多于运算符优先级所能表达的。
> 像这种点运算，它本身就可以有不同的优先级。它是它前面的语法结构来决定自己的优先级。如带圆括号的属性的优先级则比不带圆括号的要低两级。
> 所以有时用优先级来解释运算符并不是一种严谨的说法。真正严谨的还是使用产生式一级一级语法结构来描述运算的优先顺序。

- `foo()`
- `super()`
- `foo()['b']`
- `foo().b`
- foo()`abc`

___Example___

- `new a()['b']`
  - -- 这时到底是圆括号是与a先结合，然后再给new还是先跟new结合？
  由于带圆括号的new是一个Member Expression，优先级高于Call Expression,同时后面的带方括号的属性访问也因为被圆括号，
  被Call Expression拉低了优先级导致其优先级变低。所以正确的理解方式是new出来了一个a对象，然后访问了它的 b 属性。

　Call、New 和Member 这三个原本是级别差不多的。但因为要处理new后面的圆括号与谁结合的问题，因而产生了三个不同的表达式的优先级。

　**2.5 Left hand side & Right hand side**
 ___Example___

- `a.b = c`
- `a + b = c`

　可以使用a.b = c, 而不可以使用 a + b = c.
　因为 a + b 属于  Right hand side，只有 Left hand side 有资格放在等号左边。所以 Left hand side 就是根据能不能放到等号左边而来的，并不会特意去定义Right hand side。

##### 2.6 Update

- `a++`
- `a--`
- `--a`
- `++a`

　不能放在等号左边的从Update Expression 这一级开始就已经是 Right hand side。我们可以认为 Left hand side Expression几乎一定是 Right hand side Expression，在JavaScript里面没有例外。
  Right hand side Expression 是从 Update Expression开始的。Update 就是自增自减。假如写了 ++ a ++ 的话，它所表示的就是 a 是会优先与后边的自增相结合的，所以其最后的结果它是不合法的。
  下面例子语法上不合法，运行时无论谁先最后也都是不合法的。
  
 ___Example___

- `++ a ++`
- `++ (a ++)`

##### 2.7 Unary 单目运算符

- `delete a.b`
  - -- delete算是一个典型，后面必须是Reference类型才能够生效。 
- `void foo()`
  - -- void 运算符的作用是后面不管是什么东西都把它变成 undefined，该运算符其实类似于空白、回车，能起到很好的改变语法结构的作用。
- `typeof a`
- `+a`
  - -- 不会改变后面表达式的值，但是如果 a 为字符串的话，则会发生一些类型转换。
- `-a`
- `~a`
  - -- 浪线属于位运算。它把一个整数按位取反，如果不是整数，则会将其强制转换为整数。
- `!a`
  - -- 非运算，针对布尔型的运算，可以用两个非把一个任何类型的数强制转换成布尔类型。
- `await a`
  - -- await 会对后续的语法，会对更大的语法结构造成一些影响。<!-- TO DO  ……所以具体是什么影响……？Emm有时间再查证吧 -->  
  
##### 2.8 Exponental

- `**`
  - -- 唯一一个

 ___Example___

- `3 ** 2 ** 3`
- `3 ** (2 ** 3)`

### 录播 | 二、 JS表达式 | 类型转换

#### 4.Structure

#### 5.Program/Module

### 录播 | 三、 JS 语 句 | 运行时相关概念

#### 1. Statement

- Grammar
  - 简单语句
  - 组合语句
  - 声明
- Runtime
  - Completion Record
  - Lexical Environment

#### 2. Completion Record

``` JavaScript
if(x == 1)
  return 10;
```

我们需要一个数据结构来描述语句的执行结果：是否返回了？返回值是啥？等等......

### 录播 | 四、 JS 语 句 | 简单语句和复合语句

#### 1. 简单语句

- ExpressionStatement
- EmptyStatement
- DebuggerStatement
- ThrowStatement
- ContinueStatement
- BreakStatement
- ReturnStatement

#### 2. 复合语句

- BlockStatement
- IfStatement
- SwitchStatement
- IterationStatement
- WithStatement
- LabelledStatement
- TryStatement

#### 3. block

``` JavaScript
{
  ░░░░
  ░░░░
  ░░░░
}
```

- [[type]]: normal
- [[value]]: --
- [[target]]: --

#### 4. Iteration

- while( ▒▒ ) ░░░░
- do ░░░░ while( ▒▒ );
- for( ▓▓ ; ▒▒ ; ▒▒) ░░░░
- for( ▓▓ in ▒▒ ) ░░░░
- for( ▓▓ of ▒▒ ) ░░░░
- ~~for await( of )~~

<!-- DoTo -->
- var
- const / let
- in

#### 5. 标签、循环、break、continue

- LabelledStatement
- IterationStatement
- ContinueStatement
- BreakStatement
- SwitchStatement

<!-- DoTo -->
- [[type]]: break continue
- [[value]]: --
- [[target]]: label

#### 6. try

``` JavaScript
try {
  ░░░░░░░░
} catch( ▓▓▓ ) {
  ░░░░░░░░
} finally {
  ░░░░░░░░
}
```

- [[type]]: return
- [[value]]: --
- [[target]]: label

### 录播 | 五、 JS 语 句 | 声明

#### 1. 声明

- FunctionDeclaration
- GeneratorDeclaration
- AsyncFunctionDeclaration
- AsyncGeneratorDeclaration
- VariableStatement
- ClassDeclaration
- LexicalDeclaration

- function
- function *
- async function
- async function *
- var

<!-- DoTo -->
- class
- const
- let

#### 2. 预处理（pre-process）

``` JavaScript
var a = 2;
void function (){
  a = 1;
  return;
  var a;
}();
console.log(a);
```

``` JavaScript
var a = 2;
void function (){
  a = 1;
  return;
  const a;
}();
console.log(a);
```

#### 3. 作用域

``` JavaScript
var a = 2;
void function (){
  a = 1;
  {
  var a;
  }
}();
console.log(a);
```

``` JavaScript
var a = 2;
void function (){
  a = 1;
  {
  const a;
  }
}();
console.log(a);
```

### 录播 | 六、 JS结构化 | 宏任务和微任务

#### 1. 作用域1



### 录播 | 七、 JS结构化 | JS函数调用

#### 1. 作用域2

## 本周作业

## 本周总结

……对我来说这大概不是重学JavaScript，而是新学JavaScript。已经陷入有些知识点似乎曾经听过，然后有一些知识点完全不知道的局面。还有原来有些中文名称是这样，英文叫法是这样的感慨……orz。太难了。
此外这周有花时间看了一下组内其他成员的 Markdown 笔记。 这个倒是学到了。这次用 Markdown 做记录倒是也算确定了后面自己的笔记风格了。 后面可能会再进一步补充一下吧。诶。
债太多 =.=  继 StringToNumber 那个转换作业完全不行。弃疗后。经过了这三周，我基本确定自己就是做完笔记就好了。大概以后重心会放在笔记，课程视频的理解上。对我来说目前吃透是真的做不到。
只争取能通过笔记记住这些知识点吧。

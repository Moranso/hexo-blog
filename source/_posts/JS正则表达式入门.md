---
title: JS正则表达式入门
date: 2019-03-12 20:08:21
tags:
---

### 正则表达式是一种字符模式对象（RegExp）Regular Expression

1、new构造方式
var r = new RegExp(“abc”);
2、字面量方式（推荐）
var r = /abc/;

------

RegExp 对象方法

test	检索字符串中指定的值。返回 true 或 false。

var r = /abc/;
console.log(r.test("abcc")); //1

------

#### 精确匹配，/abc/

修饰符		描述
i			  执行对大小写不敏感的匹配。
g			 执行全局匹配（查找所有匹配而非在找到第一个匹配后停止,替换、提取字符串时候有用）。
m			执行多行匹配。

/abc/igm

------

非可见字符，如空格，换行等。反斜线(\)作为前缀进行转义，使用“\特殊字符”转义
\n 查找换行符  \r 查找回车符。

^  $  ．  *  +  ?  =  !  ：  |  ＼  ／  (  )  [  ]  {  } 具有特殊含义  

var r = /\n/;	//匹配一个换行
console.log(r.test("aaaaaaaaaaaaaaaaa\nb"));	 //true

var re = /.jpg/;
re.test("hahajpg"); 	//true
re.test("haha.jpg");	//true

re = /\.jpg/;
re.test("hahajpg");	 //false
re.test("haha.jpg"); 	//true

------

#### [abc] 匹配“a”“b”和“c”中的任何一个字符

var re = /[abc]/;
re.test("console");	 //true
console.log(r.test("byyyyy"));	//true
console.log(r.test("ayyybyyc"));	//true
re.test("hehe"); 	//false

------

[^abc] 除了“a”、”b”、“c”以外的任意字符，即不能单独出现“a”或”b”或“c”

console.log(re.test("console")); //1
console.log(re.test("a")); //0
console.log(re.test("b")); //0
console.log(re.test("c")); //0
console.log(re.test("a5")); //1
console.log(re.test("are")); //1

------



#### 匹配一类字符

[0-9]	查找任何从 0 至 9 的数字。
[a-z]	查找任何从小写 a 到小写 z 的字符。
[A-Z]	查找任何从大写 A 到大写 Z 的字符。
[A-z]	查找任何从大写 A 到小写 z 的字符。
[adgk]	查找给定集合内的任何字符。
[^adgk]	查找给定集合外的任何字符。
(red|blue|green)	查找任何指定的选项。

r = /[0-9]/;	//字符串中必须出现0-9其中一个，一次就行；
console.log(r.test("456789a12345"));	//true;
console.log(r.test("aaaaaaaa"));	//false;

r = /[a-zA-Z0-9]/;
console.log(r.test("A"));	//true;
console.log(r.test("a8"));	//true;

##### r = /[\^\-]/; //匹配字符串中“^”,"-"其中一个；

console.log(r.test("fasdf^131312"));//true

#### 匹配文件后缀是否是以“.jpg”,“.png”   "|" 代表或者；

r = /\.(jpg|png)/; //表示"."后面出现jpg或png;
console.log(r.test("xxx.jpg"));//true
console.log(r.test("xxx.png"));//true
console.log(r.test("xxx.gif"));//false
console.log(r.test("xxxpng"));//false
console.log(r.test("xxx.pngggggg"));//true



------

选择（其一）

字符“|”用于分隔供选择的字符，“|” 可以理解为或者的意思；
比如：var re = /jpg|png|gif/; //匹配字符串中jpg、png、gif; 字符串中只需要匹配其中一个就ok了；
      re.test(“xxx.jpg”);//true

------



#### 指定位置（限定位置）

^n	匹配任何开头为 n 的字符串。
n$	匹配任何结尾为 n 的字符串。
(?=n)	匹配任何其后紧接指定字符串 n 的字符串。
(?!n)	匹配任何其后没有紧接指定字符串 n 的字符串。

r = /\.(jpg|png)$/;
console.log(r.test("xxx.pngggggg"));//false
r=/[1-9]/;
r.test("a3399dsfd");//1
r=/^[1-9]/;
r.test("03399dsfd");//0
r.test("13399dsfd");//1
//QQ号规则，不能以0开头的5-12位数字
r=/^[1-9]\d{4,11}/
r.test("13399dsfd");//1
r=/^[1-9]\d{4,11}$/
r.test("13399dsfd");//0
r.test("1339955656");//1



------

#### 元字符类

.	查找单个字符，除了换行和行结束符。
\w	查找单词字符。  //[a-zA-Z0-9_]
\W	查找非单词字符。
\d	查找数字。
\D	查找非数字字符。
\s	查找空白字符。
\S	查找非空白字符。
\b	匹配单词边界。
\B	匹配非单词边界。

var r = /./;
console.log(r.test("("));//true

r = /\w/; //[a-zA-Z0-9_];//单词字符，包含_
console.log(r.test("@"));//false

r = /\W/; //[^a-zA-Z0-9_];//非单词字符。
console.log(r.test("%"));//true

r = /\d/;//[0-9]数字
console.log(r.test("0.5"));//true

r = /\D/;//[^0-9]非数字
console.log(r.test("0.5"));//true

r = /\s/; //空白字符
console.log(r.test("5a "));//true

r = /\S/; //非空白字符
console.log(r.test("5 abc"));//false
console.log(r.test("5abc"));//true



------

#### 量词：限定字符（重复次数）

n+
匹配任何包含至少一个 n 的字符串。
n*
匹配任何包含零个或多个 n 的字符串。
n?
匹配任何包含零个或一个 n 的字符串。
n{X}
匹配包含 X 个 n 的序列的字符串。
n{X,Y}
匹配包含 X 或 Y 个 n 的序列的字符串。
n{X,}
匹配包含至少 X 个 n 的序列的字符串。

列如：
/\d{2，4}/     //匹配2-4个数字
/\w{3}\d?/     //匹配3个单词和一个可选数字
/\s+js\s+/     //匹配前后各带一个或多个空格的字符串”js”
var r = /\d\d\d\d\d\d\d\d\d\d/;//连续10个数字
console.log(r.test("0123456789aaa"));//true

r = /\d+/;
console.log(r.test("abc1"));//1
console.log(r.test("abc11"));//1

r = /\d*/;//零个或多个 n的字符串
console.log(r.test("abc"));//1
console.log(r.test("abcfasdf23423423542352345"));//1

r = /\d?/;//匹配任何包含零个或一个 n 的字符串。
console.log(r.test("abc1"));//1

r = /\d{3}/;//字符串中连续出现3个数字；
console.log(r.test("a123"));//1

r = /\d{5,12}/;//字符串中连续5-12个数字；
console.log(r.test("123456789011144444444"));//1

r = /\d{5,}/;//字符串中连续5个以上数字；
console.log(r.test("1234a545679"));//1

//匹配qq
r = /[1-9]\d{4,11}/;
console.log(r.test("012345"));//true //不能只看整体，要依次看匹配情况

------

#### 贪婪匹配与非贪婪匹配

#### 默认重复匹配是贪婪匹配，修改为非贪婪匹配只须量词后面加一个?号即可；

例子：
  var s = “gggg<aaa@itsource.cn>和<bbb@itsource.cn>hhhhh”;

  var r = /<.*>/;
  console.log(r.test(s));
  console.log(r.exec(s));
  console.log(r.exec(s).length);
  console.log(r.exec(s)[0]);

  r = /<.*?>/;
  console.log(r.test(s));
  console.log(r.exec(s));
  console.log(r.exec(s).length);
  console.log(r.exec(s)[0]);

  // g全局匹配，匹配了第一个，然后接着继续匹配，执行一次匹配一次
  r = /<.*?>/g;
  console.log(r.exec(s));
  console.log(r.exec(s)[0]);

------

#### 分组

正则表达式中的圆括号有多种作用，可以把单独的项组合成子表达式，以便可以处理一个；

像处理一个独立的单元那样用“|”、  “*”、  “+”或者“？”等来对单元内的项进行处理。

例如：/java(script)?/可以匹配字符串“java”，其后可以有“script”也可以没有

正则表达式中，圆括号的另一个作用是在完整的模式中定义子模式。当一个正则表达式成功地和目标字符串相匹配时，可以从目标串中抽出和圆括号中的子模式相匹配的部分。

一个或多个小写字母后面跟随了一位或多位数字，则可以使用模式 /[a-z]+\d+/
如果将模式的数字部分放在括号中/[a-z]+(\d+)/，就可以从检索到的匹配中抽取数字了

例子：

//正则表达式中的圆括号有多种作用-可以把单独的项组合成子表达式，然后可以这个这个子表达式使用量词；
var r  = /(hehe){4}/;
console.log(r.test("yyyyy:hehehehehehe"));

//例如，假定我们正在检索的模式是一个或多个小写字母后面跟随了一位或多位数字，则可以使用模式/[a-z]+\d+/。
var r = /[a-z]\d+/; //描述一个字符串是以a-z开头，后面紧跟着一个或多个数字
console.log(r.test("a123"));

//但假定我们真正关心的是每个匹配尾部的数字，那么如果将模式的数字部分放在括号中/[a-z](\d+)/，就可以从检索到的匹配中抽取数字了。
var r = /[a-z](\d+)/;
var arr = r.exec("a88888");
arr[1] //88888 ; //返回的数组中取二个元素，数组中的第二个元素就是正则中（\d+）的匹配；

//引用()匹配的字符串；  \1引用第一个括号"()"中匹配到的内容；
r = /(\w)\1{2}/;
console.log(r.test("AAA"));



------

#### RegExp 对象方法

test	检索字符串中指定的值。返回 true 或 false。

var r = /^abc$/;
console.log(r.test("abcc")); //0



exec(str)：用于使用正则表达式模式在指定字符串中进行匹配查找，并将查找结果以数组形式返回,没有找到就返回null
		exec()方法的返回值为Array类型，如果找到了对应的匹配，则返回数组的成	员如下：
		索引0：存放第一个匹配的子字符串。
		属性index：匹配正则表达式在目标字符串中的起始索引位置。
		属性input：整个字符串对象(stringObject)。
		属性length：长度

//g表示从整个字符串中查找，但是每次执行exec方法只查找一次。
//如果你需要在整个字符串中匹配所有，那么请加"g"全局。

r =/\d+/g;
        	
//返回一个数组，数组的第一个元素就是匹配的值。 
var arr = r.exec("a123a456");
console.log(arr[0]);
console.log(arr.index);//匹配字符串位置

arr = r.exec("a123a456");
console.log(arr[0]);
console.log(arr.index);//匹配字符串位置

r=/\d+/g;

while(true){
	var arr = r.exec("a123a456a789");
	if(arr!=null){//判断是否有匹配到字符串。
		console.log(arr[0]);
	}else{
		break;
	}
}

------

#### 支持正则表达式的 String 对象的方法

search	检索与正则表达式相匹配的值。
match	找到一个或多个正则表达式的匹配。
replace	替换与正则表达式匹配的子串。
split	把字符串分割为字符串数组。

//replace 替换与正则表达式匹配的子串。
//参数1：原字符， 参数1：替换后的字符串
var s = "1*2*3*4*5*6";
s = s.replace(/\*/g,"_"); //g:全部替换
console.log(s);

//split 把字符串分割为字符串数组
var s = "hello world welcome";
console.log(s.split(/\s+/));//s表示空格
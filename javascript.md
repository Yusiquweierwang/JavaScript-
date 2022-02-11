#JavaScript
##1.基本语法

```javascript
// 1.定义变量  变量类型 变量名 = 变量值；
var num = 1;
var name = "yusiquweierwang";
var score = 66;
// 2.条件控制
if (2 > 1) {
  alert("female");
} else if (score > 40) {
  alert("fe");
}
//javaScript严格区分大小写

//console.log()在浏览器控制台打印变量

//javascript 不区分小数和整数，number,Number
123; //整数123
123.3; //浮点数123.3
1.2e2 - //科学计数法
  99; //复数
NaN; //not a number
Infinity; //无穷大数

//   字符串'abc' "bad"
//布尔值
//逻辑运算
//比较运算符
//==:类型不一样，值一样，true
//===:类型一样，值一样，true
//NaN===NaN:与所有数值都不相等，isNaN来判断

//浮点数问题：console.log(1/3) false  -->因为存在精度问题
console.log(1 / 3) === console.log(1 - 2 / 3);
console.log(Math.abs(1 / 3 - (1 - 2 / 3)) < 0.000001);

//undefined 未定义
// null空

var arr = [1, 2, 3, 4, 5, "hello", null, true];
//java中必须列相同类型的对象，javascipt中不需要
//取数组下标，如果越界了，会:-->undefined

//   对象：对象是大括号，数组是中括号
var person = {
  name: "yusiquweierwang",
  age: 3,
  tags: ["js", "java", "web", "..."],
};
```

严格检查模式：'use strict';

### map()和 set()

```javascript
//map()
var map = new Map([
  ["Tom", 100],
  ["Jack", 90],
  ["Smith", 74],
]);
var Tom_name = map.get("Tom"); // 通过key 获得value
map.set("admin", 23);
console.log(Tom_name); //输出100
var admin = map.get("admin");
console.log(admin); //输出23
//set:无序不重复的集合
var set = new Set([3, 1, 1, 1, 1]); // set 可以去重
set.add("more", 2);
```

遍历 map

```javascript
var map = new Map([
  ["tom", 20],
  ["jack", 30],
  ["mark", 90],
]);
for (let [key, value] of map.entries()) {
  console.log(key + " " + value);
}
```

##iterator 迭代器
###for in:打印值的下标
###for of:打印值

##函数
###1.定义函数

```javascript
function abs(x) {
  //不存在参数时的规避问题：抛出异常；
  if (typeof x !== "number") {
    throw "Not a Number";
  }

  //arguments代表传递进来的所有参数是一个数组
  console.log("x=>" + x);
  for (var i = 0; i < arguments.length; i++) {
    console.log(arguments[i]);
  }

  if (x > 0) {
    return x;
  } else {
    return -x;
  }
}
```

###rest 参数

```javascript
//原来
function aaa(a, b) {
  console.log("a=>" + a);
  console.log("b=>" + b);
  console.log("a=>" + b);
}

//es6新特性,rest参数只能写在最后面，必须用...rest标识
function aaa_a(a, b, /*此处必须加*/ ...rest) {
  console.log("a=>" + a);
  console.log("b=>" + b);
  console.log(rest); //剩余组成一个数组
}
```

##变量的作用域 1.假设在 javasript 中函数查找变量从自身函数开始，由“内”向“外”查找，假设外部存在同名，，则内部函数会屏蔽外部函数

```javascript
var x = 1;
function f() {
  console.log(x);
}
f();
console.log(x);
```

2.全局变量 window
默认所有的全局变量，都会自动绑定在 window 对象下。
规范：由于所有的全局变量都会绑定到 window 上 ，如果不同的 js 文件，使用了相同的全局变量，则会冲突。
定义唯一全局变量，把自己代码全部放入自己定义的唯一空间名字中，降低全局命名冲突问题-->jQuery==$()

```javascript
var yusiquweierwang = {}; //定义唯一全局变量
yusiquweierwang.name = "Jiazhi Yu";
yusiquweierwang.add = function (a, b) {
  return a + b;
};
```

##方法
即把函数放在 对象的内部，对象只有两个东西：属性和方法。
例：判断今年

```javascript
var yusi = {
  name: "qudaer",
  birth: 3020,
  age: function () {
    //今年-出生的年
    var now = new Date().getFullYear();
    return now - this.birth;
    //this 无法指向，默认只想调用它的对象
  },
};
```

call() 方法分别接受参数。

apply() 方法接受数组形式的参数。

###Date()
var now = new Date();
now.getFullYear(); //年
now.getMonth(); //get 月
now.getDay();
now.getHours();

##class 继承

```javascript
//ES6之后定义一个类，类中含属性和方法
class Student {
  constructor(name) {
    this.name = name;
  }
  hello() {
    alert("hello");
  }
}

//继承
class Pupils extends Student {
  constructor(name, grade) {
    //super关键字用于访问和调用一个对象的父对象上的函数。
    super(name);
    this.grade = grade;
  }
  myGrade() {
    alert("我是一名小学生");
  }
}

var xiaoming = new Student("xiaoming");
var xiaohong = new Student("xiaohong");
```

##原型

```javascript
//创建一个user对象
var user = {
  name: "yusiquweierwang",
  age: 33,
  sex: "male",
  run: function () {
    console.log(this.name + "run...");
  },
};

//创建xiaoming对象，此时不能run
var xiaoming = {
  name: "xiaoming",
};
//__proto__此时xiaoming能run了
xiaoming.__proto__ = user;

var bird = {
  fly: function () {
    console.log(this.name + "fly");
  },
};

//xiaoming能fly了
xiaoming.__proto__ = bird;
```

###JSON
JSON 是 JS 对象的字符串表示法，它使用文本表示一个 JS 对象的信息，本质是一个字符串。
如

```javascript
var obj = { a: "Hello", b: "World" }; //这是一个对象，注意键名也是可以使用引号包裹的

var json = '{"a": "Hello", "b": "World"}'; //这是一个 JSON 字符串，本质是一个字符串
//1.对象转化为json字符串：stringify()
var jsonUser = JSON.stringify(user);

//2.json字符串转化为对象:parse()
var jsonParseUser = JSON.parse(jsonUser);
```

##DOM

###获得文档树的节点

```javascript
<dl id="app">
      <dt>java</dt>
      <dd>JavaSE</dd>
      <dd>JavaEE</dd>
    </dl>
    <script>
      var dl = document.getElementById("app");
```

# 对象

## 谈谈你对面向对象的理解

> 面向对象：是一种编程思想。提出需求，抽取出对象，调用对象相关的属性或者方法。抽取出对象及特征和行为，通过代码实现对象调用对应的属性和方法、特征---->属性,行为--->方法,对象的类型---->类(类别)
>
> 对象：看得见，摸得到，具体特指的某个东西。（不是指类别）,具有属性或者方法，特指的某个事物
>
> 面向对象的特性：封装、继承、多态，(抽象性)

```js
// 先定义手机对象的类型(通过构造函数来定义,通过new构造函数,来实例化对象)
// 构造函数
function Phone(color, weight) {
  // 手机的对象的特征---->属性
  this.color = color;
  this.weight = weight;
  // 手机的对象的行为---->方法
  this.call1 = function () {
    console.log("您好,我是illion");
  };
}
// 通过构造函数创建对应的一个具体的对象(实例化对象)
// 实例化对象的同时进行属性的初始化
var phone = new Phone("黑色", "300g");
phone.call1();
```

## 常见的实例化对象的方法

1、字面量

```js
var obj = {};
```

2、通过工厂模式创建对象

```js
function createObject(name, age) {
  var obj = new Object();
  obj.name = name;
  obj.age = age;
  return obj;
}
var obj1 = createObject("小明", 10);
var obj2 = createObject("小红", 20);
console.log(obj1, obj2);
```

3、构造函数的方式创建对象

```js
function Person(name, gender) {
  this.name = name;
  this.gender = gender;
  this.sayHi = function () {
    console.log("您好,我是:" + this.name);
  };
}
var per = new Person("小明", "男");
per.sayHi();
console.log(per);
```

4、类的方式

```js
class Student {
  // 构造器,构造器中的属性,最终都是在实例对象上的
  constructor(name, age, gender) {
    this.name = name;
    this.age = age;
    this.gender = gender;
  }
  // 在原型上
  sayHi() {
    console.log(`您好,我是${this.name},今年${this.age}岁了,是${this.gender}生`);
  }
  // class 中书写方法的时候,如果方法使用的是 = 赋值符号的方式来定义的,那么方法在实例上

  // 在实例上
  eat = () => {
    console.log("吃东西啊");
  };
  // play 方法在原型上还是在实例上? 实例上的
  play = function () {
    console.log("一起玩游戏啊");
  };
}
// 实例化对象
var stu = new Student("小白", 20, "男");
stu.sayHi();
stu.eat();
console.dir(stu);
```

```js
function Person(name, age) {
  this.name = name;
  this.age = age;
  this.sayHi = function () {
    console.log("您好啊");
  };
}
Person.prototype.eat = function () {};
var p1 = new Person("小明", 20);
var p2 = new Person("小明", 20);
// true还是false?----false,两个对象都有自己的sayHi方法,
//如果有多个对象,那么就会出现多个对象占用多块空间,用来存储自己的方法,浪费内存,
//既然方法中的内容都是一样的,那么方法就应该放在原型上,占用一块空间,节省内存空间,实现数据共享
console.log(p1.sayHi === p2.sayHi);
```

5、简单的单例模式创建对象

> 单例模式：不管该对象创建多少次，实际上，最终对象只有一个

```js
function createObj() {
  var instance = null;
  return function (name) {
    if (!instance) {
      // 创建对象
      instance = new Object();
      // 初始化对象的属性值
      instance.name = name;
    }
    // instance 对象 已经创建完毕了, 此时是存在的
    return instance;
  };
}
var getObj = createObj();
var obj3 = getObj("小明");
var obj4 = getObj("小红");
var obj5 = getObj("小红");
var obj6 = getObj("小红");
var obj7 = getObj("小红");
var obj8 = getObj("小红");
var obj9 = getObj("小红");
console.log(obj3, obj4);
console.log(obj3 === obj4); //ture
// 一个页面中有多个轮播图的效果,如果说此时为了实现轮播图的效果,那么就会创建对应的多个swiper的对象,
// 此时可以使用单例模式的创建只创建一个对象,节省空间,
// better-scroll的插件----单例模式
```

## new 一个对象做了哪几件事

    1、开辟新的内存空间(申请一块空闲空间),用来存储实例化的对象
    2、设置this为当前对象(改变this的指向)
    3、初始化属性或者方法的值
    4、返回this这个实例对象

```
1. 对象.属性名字
2. 对象['属性名字']
3. 什么时候使用对象[属性名字]的写法
   - 不确定属性名字是什么(属性名字是变量)
   - 属性名字不太规范的时候
```
```
    js是弱类型语言,声明变量都用var
    js是脚本语言 直接执行
    js是解释性语言 直接解释
    js是动态类型语言 变量在执行的时候才知道具体的类型,对象没有这个属性,点了,就有了
    js是单线程语言 执行的时候安装一定的顺序,之前的代码执行完毕后,后面才执行
    js是基于对象的语言,最终所有的对象都指向了object
```
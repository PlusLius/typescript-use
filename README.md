# typescript-use

## 基本数据类型

```ts

//基本套路 A:类型 = 类型 ？值 : 报错
//函数类型 function 函数名(参数:类型):返回值类型
//数组  变量:Array<类型> = [值，...]

//布尔类型
let a:boolean = false

//数字类型
let b:number = 10

//字符串
let c:string = '123'

//数组类型
let arr1:number[] = [4,5,6]
let arr2:Array<number> = [7,8,9]

//元组类型
let tuple:[string,number] = ['123',5]

//枚举
enum Cat {
    miao='miao',
    mu='mu'
}
console.log(Cat.mu)

//任意类型
let ok:any = 123

//null or undefined
let x:number
x = 1
x = undefined
x = null

//void类型
function test(obj:string):void{
    console.log(obj)
}

test('123')

//never类型 表示不会出现的值
function test2(obj:string):never{
    throw new Error(obj)
}

//联合类型
let d:string | number
d = '21'
d = 123


```

## 函数

```ts
//函数定义,可选参数和返回类型,剩余参数
function hello(name:string,age?:number,...reset:number[]):void{
    console.log(name)
}
hello('plus')

//函数重载,在Java中的重载，指的在TypeScript中，表现为给同一个函数提供多个函数类型定义
let obj:any = {}
function a1(val:string):void
function a1(val:number):void
function a1(val:any):void{
    if(typeof val === 'number'){
        obj.age = val
    }else {
        obj.name = val
    }
}
a1('plus')
a1(1)
a1(true)
console.log(obj)
```
## 类

```ts
//类,存取器,readonly修饰符
class Person{
    //readonly name:string;
    name:string;
    constructor(name:string){
        this.name = name
    }
    getName():void{
        console.log(this.name)
    }
    get myname() {
        return this.name;
    }
    set myname(value) {
        this.name = value;
    }
}
let p1 = new Person('a')

//继承
class Student extends Person{
    age:number
    constructor(name:string,age:number){
        super(name)
        this.age = age
    }
    getAge():number{
        return this.age
    }
}

let s1 = new Student('plus',24)
console.log(s1.getAge())

//类修饰符,静态属性和静态方法
class Father {
    static className = '1'
    public name: string;  //类里面 子类 其它任何地方外边都可以访问
    protected age: number; //类里面 子类 都可以访问,其它任何地方不能访问
    private money: number; //类里面可以访问， 子类和其它任何地方都不可以访问
    constructor(name:string,age:number,money:number) {//构造函数
        this.name=name;
        this.age=age;
        this.money=money;
    }
    getName():string {
        return this.name;
    }
    setName(name:string): void{
        this.name=name;
    }
}
class Child extends Father{
    constructor(name:string,age:number,money:number) {
        super(name,age,money);
    }
    desc() {
        //console.log(`${this.name} ${this.age} ${this.money}`);
    }
}

let child = new Child('plus',10,1000);
console.log(child.name);
// console.log(child.age);
// console.log(child.money);

//抽象类 抽象描述一种抽象的概念，无法被实例化，只能被继承 无法创建抽象类的实例 抽象方法不能在抽象类中实现，只能在抽象类的具体子类中实现，而且必须实现
abstract class Animal3 {
    name:string;
    abstract speak();
}
class Cat extends Animal3{
    speak(){
        console.log('喵喵喵');
    }
}
let cat = new Cat();
cat.speak();

abstract class Animal5{
    name:string;
    constructor(name:string){
      this.name = name;
    }
    abstract speak();
  }
  interface Flying{
      fly()
  }
  class Duck extends Animal5 implements Flying{
      speak(){
          console.log('汪汪汪');
      }
      fly(){
          console.log('我会飞');
      }
  }
  let duck = new Duck('plus');
  duck.speak();
  duck.fly();

//继承 or 多态
//继承（Inheritance）子类继承父类，子类除了拥有父类的所有特性外，还有一些更具体的特性
//多态（Polymorphism）由继承而产生了相关的不同的类，对同一个方法可以有不同的响应
class Animal7{
    speak(word:string):string{
        return 'Animal: '+word;
    }
}
class Cat7 extends Animal7{
    speak(word:string):string{
        return 'Cat:'+word;
    }
}
class Dog7 extends Animal7{
    speak(word:string):string{
        return 'Dog:'+word;
    }
}
let cat7 = new Cat7();
console.log(cat7.speak('hello'));
let dog7 = new Dog7();
console.log(dog7.speak('hello'));

//重写 or 重载
//重写是指子类重写继承自父类中的方法
//重载是指为同一个函数提供多个类型定义
class Cat6 extends Animal6{
    speak(word:string):string{
        return 'Cat:'+word;
    }
}
let cat6 = new Cat6();
console.log(cat6.speak('hello'));

function double(val:number):number
function double(val:string):string
function double(val:any):any{
  if(typeof val == 'number'){
    return val *2;
  }
  return val + val;
}

let r = double(1);
console.log(r);
```

## 接口

```ts
/*
接口一方面可以在面向对象编程中表示为行为的抽象，另外可以用来描述对象的形状
接口就是把一些类中共有的属性和方法抽象出来,可以用来约束实现此接口的类
一个类可以继承另一个类并实现多个接口
接口像插件一样是用来增强类的，而抽象类是具体类的抽象概念
一个类可以实现多个接口，一个接口也可以被多个类实现，但一个类的可以有多个子类，但只能有一个父类
*/
interface Speakable{
    speak():void;
    name?:string
}

let speakman:Speakable = {
    name:'123',
    speak(){}
}

//接口可以在面向对象编程中表示为行为的抽象
interface Speakable{
    speak():void
}
interface Eatable{
    eat():void
}

class Person implements Speakable,Eatable {
    speak(){
        console.log('Person5说话');
    }
    eat(){

    }
}

class TangDuck implements Speakable{
    speak(){
        console.log('TangDuck说话');
    }
    eat(){}
}

//无法预先知道有哪些新的属性的时候,可以使用 `[propName:string]:any`,propName名字是任意的
interface Person {
    readonly id: number;
    name: string;
    [propName: string]: any;
  }
  
let p1 = {
    id:1,
    name:'plus',
    age:10
  }

//接口继承
interface Speakable{
    speak():void
}
interface SpeakChinese extends Speakable{
    speakChinese():void
}
class Person5 implements SpeakChinese{
    speak(){
        console.log('Person5')
    }
    speakChinese(){
        console.log('speakChinese')
    }
}

//修饰
interface Tom {
    readonly id:number;
    name:string
}
let tom:Tom = {
    id :1,
    name:'plus'
}
//  tom.id = 1;

//对方法传入的参数和返回值进行约束
interface discount{
    (price:number):number
}
let cost:discount = function(price:number):number{
    return price * .8;
}

//可索引接口
//对数组和对象进行约束
//userInterface 表示：只要 index 的类型是 number，那么值的类型必须是 string
//UserInterface2 表示：只要 index 的类型是 string，那么值的类型必须是 string
interface UserInterface {
    [index:number]:string
}
let arr:UserInterface = ['plus1','plus2'];
console.log(arr);
  
interface UserInterface2 {
    [index:string]:string
}
let obj2:UserInterface2 = {name:'plus'};

//类接口
interface Speakable2{
    name:string;
    speak(words:string):void
}
class Dog implements Speakable2{
     name:string;
     speak(words){
      console.log(words);
     }
}
let dog=new Dog();
dog.speak('汪汪汪');

//在 TypeScript 中，我们可以用 interface 来描述类
//同时也可以使用interface里特殊的new()关键字来描述类的构造函数类型
class Animala{
    constructor(public name:string){
      
    }
}
interface WithNameClass{
    new(name:string):Animala
}
function createAnimal(clazz:WithNameClass,name:string){
    return new clazz(name);
}
let aaa = createAnimal(Animala,'plus');
console.log(aaa.name);
```

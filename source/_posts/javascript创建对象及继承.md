---
title: javascript创建对象及继承
date: 2016-07-29 11:02:46
tags: 
  - javascript
categories:
  - 学习笔记
  - javascript
---
本文介绍JavaScript面向对象编程中的创建对象和继承的实现，主要来自《JavaScript高级程序设计》。
<!-- more -->

# 对象的创建

1. 工厂模式

		function Person(name,age){
			var o = new Object();
			o.name = name;
			o.age = age;
			o.getName = function(){
			console.log(this.name);
			}
			return o;
		}
		var person = Person("lily",15);

 缺点：无法识别对象的类型

2. 构造函数模式

		function Person(name,age){
			this.name = name;
			this.age = age;
			this.getName = function(){
				console.log(this.name);
			}
		}
		var person = new Person("lily",15);

	注意：如何不通过new调用，则this指向window

	缺点：每个方法需要在每个实例上都重新创建一遍。若将方法移出，则当方法多时，需要定义多个全局函数，破坏封装性。

3. 原型模式

		function Person(){}
		Person.prototype.name = "lily";
		Person.prototype.age = 15;
		Person.prototype.getName =  function(){
			return this.name;
		};
		var person = new Person；

	缺点：（1）所有实例的默认属性值相同
	  （2）当属性中有引用类型时，也会共享。

4. 组合构造函数模式

	   function Person(name,age){
			this.name = name;
			this.age = age;
		}
		Person.prototype.getName =  function(){
			console.log(this.name);
		};
		var person = new Person("lily",15);

5. 动态原型模式

		function Person(name,age){
			this.name = name;
			this.age = age;
			if(typeof this.getName!= "function"){
				Person.prototype.getName = function(){
					console.log(this.name);
				}
			}
		}

	var person = new Person("lily",15);

6. 寄生构造函数模式

	   function Person(name,age){
			var o = new Object();
			o.name = name;
			o.age = age;
			o.getName = function(){
				console.log(this.name);
			}
			return o;
		}

		var person = new Person("lily",15);

	缺点：无法判断对象类型

7. 稳妥构造函数模式

		function Person(name,age){
			var o = new Object();
			o.name = name;
			o.age = age;
			o.getName = function(){
				console.log(name);
			}
			return o;
		}

		var person = Person("lily",15);

	与寄生构造函数模式的区别：（1）不引用this（2）创建对象不使用new
	缺点：无法判断类型

# 实现继承的方式

1. 原型链

		function SuperType(){
			this.property = true;
		}

		SuperType.prototype.getSuperValue = function(){
			return this.property;
		}

		function SubType(){
			this.subProperty = false;
		}
		SubType.prototype = new SuperType();
		SubType.prototype.getSubValue = function(){
			return this.subProperty;
		}

	缺点：（1）引用类型的属性：在通过原型继承时，原型实际上会变成另一个类型的实例，故原来实例中的属性会变成新的对象的原型中的属性。
	  （2）在创建子类型时，无法向超类型的构造函数中传递参数。

2. 借用构造函数

		function SuperType(){
			this.property = true;
			this.getSuperValue = function(){
				return this.property;
			}
		}

		function SubType(){
			SuperType.call(this);
		}

3. 组合继承

		function SuperType(){
			this.property = true;
		}
		SuperType.prototype.getSuperValue = function(){
			return this.property;
		}

		function SubType(){
			SuperType.call(this);
		}
		SubType.prototype = new SuperType();
		SubType.prototype.getSubValue = function(){
			return this.subProperty;
		}

4. 原型式继承（相当于ES5中的Object.create()）

	    function object(o){
	    	function F(){};
	    	F.prototype = o;
	    	return new F();
	    }

5. 寄生式继承(增强对象)

		function CreateAnother(o){
			var another = object(o);
			another.sayName = function(){
				console.log(this.name);
			}
			return another;
		}

6. 寄生组合式继承

		function SuperType(){
			this.property = true;
		}
		SuperType.prototype.getSuperValue = function(){
			return this.property;
		}

		function SubType(){
			SuperType.call(this);
		}
		inheritPrototype(subType,superType);
		SubType.prototype.getSubValue = function(){
			return this.subProperty;
		}
		function inheritPrototype(subType,superType){
			var prototype = object(superType.prototype);
			prototype.constructor = subType;
			SubType.prototype = prototype;

		}
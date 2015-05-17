# 闭包 Closure

## 引子

`JavaScript` 中的闭包源于它的两个特殊性质

* All functions are objects and have a scope chain associated with them 函数被看做Object，拥有作用域链
* Lexical Scoping 词法作用域

### Scope chain

我们先写一个嵌套函数

```
window.scope = "level 0";
var s2 = "s2";
function scopeFA() {
	var scope = "level 1";
	function scopeFB() {
		console.log(scope, s2);  // "level 1", "s2" 
	}
	scopeFB();
	console.log(scope);          // "level 1"
}
scopeFA();
console.log(scope);              // "level 0"
```

### The lexical scoping rules for nested functions

我们来看以下的代码。

```
var scope = "global scope";
function checkScope() {
	var scope = "local scope";
	function subFunc() {
		return scope;
	}
	return subFunc();
}
checkScope();
```

现在把上面的代码稍加修改。

```
var scope = "global scope";
function checkScope() {
	var scope = "local scope";
	function subFunc() {
		return scope;
	}
	return subFunc;
}
checkScope()();
```

## Advantages of closure

* 希望一个变量长期驻扎在内存当中
* 避免全局变量的污染
* 私有成员的存在

下面我们来看闭包的基本方式。

## Global variable

```
var n = 0;
var count = function() {
	return n++;
}
count();    // => 0
count();    // => 1
```

## Private variable

```
var n = 1;
var count = function() {
	var n = 0;
	return n;
}
count();    // => 0
n;          // => 1
```

## Alter private variable

```
var n = 1;
var count = function() {
	var n = 0;
	return function() {
		return n++;
	}
}
var counter = count();
counter();    // => 0
n;            // => 1
counter();    // => 1
counter();    // => 2
n;            // => 1
```

## Function expression

```
var counter = (function() {
	var n = 0;
	return function() {
		n++;
	};
}());
counter();
```

## Private property

```
var counter = (function() {
	var n = 0;
	var count = function() {
		return n++;
	}
	return function() {
		count();
	}
}());
counter();
```

## Nested functions as closures

有时候我们不希望包中仅有一个嵌套函数。

```
var counter = function() {
	var n = 0;
	return {
		count: function() {
			return n++;
		},
		reset: function() {
			n = 0;
		}
	};
}
```

## A simple demo

```
var n = 0;
for(i = 0; i < 5; i++) {
	n++;
	setTimeout(function() {
			console.log(n);
	}, 0);
}
```

```
var n = 0;
for(i = 0; i < 5; i++) {
	n++;
	setTimeout(function(n) {
			console.log(n);
	}(n), 0);
}
```

## Private property accessor methods using closures

```
var storage = {};
function addPrivateProperty(o, name, predicate) {
	var value;
	
	o["get" + name] = function() {
		return value;
	};
	
	o["set" + name] = function(v) {
		if(predicate && !predicate(v)) {
			throw Error("set" + name + ": invalid value " + v);
		} else {
			value = v;
		}
	};
}

addPrivateProperty(storage, "Name", function(x) {
	return typeof x === "string";
});
addPrivateProperty(storage, "Age", function(x) {
	return typeof x === "number";
});

storage.setName("Rijn");
storage.setAge(18);

console.log(storage.getName(), storage.getAge());

storage.setName(18);
```

## Another simple demo

这是一个冬天用来取暖的程序

```
var n = 0;
for(i = 0; i < 5e5; i++) {
	n++;
	setTimeout(function(n) {
			console.log(n);
	}(n), 0);
}
```

## Disadvantage

* 由于闭包会使得函数中的变量都被保存在内存中，内存消耗很大，所以不能滥用闭包，否则会造成网页的性能问题，在IE中可能导致内存泄露。解决方法是，在退出函数之前，将不使用的局部变量全部删除。
* 闭包会在父函数外部，改变父函数内部变量的值。所以，如果你把父函数当作object使用，把闭包当作它的Public method，把内部变量当作它的Private value，这时一定要小心，不要随便改变父函数内部变量的值。

## Garbage collecation

### Reference

### Memory leakage in IE

```
function closure(){
    var oDiv = document.getElementById('oDiv');
    oDiv.onclick = function () {
        alert('oDiv.innerHTML');
    };
}
```

```
function closure(){
    var oDiv = document.getElementById('oDiv');
    var test = oDiv.innerHTML;
    oDiv.onclick = function () {
        alert(test);
    };
    oDiv = null;
}
```

## Final

```
var name = "trigkit4";
var student = {
	name : "Rijn",
	getName : function(){
		return function(){
			return this.name;
		};
	}
};
console.log(student.getName()());
```

## Thanks
* `Rijn`
* `2015.05.18`

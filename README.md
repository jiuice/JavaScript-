### 全局作用域

1. 直接在 script 标签中的代码，都在全局作用 
2. 全局作用域在打开页面时创建，在关闭时销毁。
3. 全局作用域中有一个全局对象 window 。它由浏览器创建我们可以直接使用。
4. 在全局作用域中：创建的变量都会作为window属性保存，创建的函数都会作为window对象方法保存。
5. 全局变量在页面的任何位置都可以被访问到。
6. 使用 var、function声明变量和方法时都会出现声明提前的特性。（即，先声明变量。然后在声明的源代码处赋值）

### 函数作用域

1. 函数作用域在调用函数时创建，在函数执行完毕后销毁。
2. 每调用一次函数就会创建一个新的函数作用域，它们之间是相互独立的。
3. 函数作用域中可以访问到全局作用中的变量，全局作用域中无法访问到函数作用域的变量。
4. 当在函数作用域操作一个变量时 ：首先在自身的作用域中寻找，如果有就直接用，没有则向上一级的作用域中寻找，如果在全局作用域中任然没有找到，则会报错。
5. let 关键字：其声明的变量只在 let 命令所在的代码快 {} 内有效，在 {} 之外不能访问。有效防止了 块级作用域中变量对作用域外对象的影响。
6. 在函数作用域内访问同名的全局变量：使用 window."变量名" 的方法。

### this关键字

* 解析器在调用函数每次都会向函数内部传递进一个隐含的参数。这个隐含的参数就是this，this指向的是一个对象。这个对象我们称为函数执行的上下文对象。
* 根据函数的调用方式的不同，this指向不同的对象。
  1. 以函数的形式调用时，this代表window对象。
  2. 以方法的形式调用时，this代表调用方法的那个对象。
  3. 以构造方法形式调用时，this代表新创建的那个实例对象。

### 构造函数

1. 构造函数就是一个普通的函数，创建的方式和普通函数没有区别。

2. 一般创建的构造函数，在函数名上一般首字母大写。

   +++

3. 构造函数和普通函数的区别就是调用方式的不同：普通函数直接调用，而构造函数使用 new 关键字调用。

4. 构造函数的执行流程：

   1. 立即创建一个新的对象。
   2. 将新建的对象设置为函数中this，在构造函数中可以使用this来引用新建的对象。
   3. 逐行执行函数中的代码。
   4. 将新建的对象作为返回值返回。

5. 使用同一个构造函数创建的对象，我们称之为一类对象，也将一个构造函数称位一个类。通过构造函数创建的对象，也称之为该类的实例。

6. instanceof 关键字可以检查创建的对象是否是一个类的实例，是：返回true；否，返回false；

   1. 任何对象的子类，(对象 instanceof Object) 其结果均是 true。

   <b>补充：</b>

   1. 在构造函数中创建方法，构造函数每创建一次就会创建一个新的方法。
   2. 每个创建的构造方法，在调用的内部方法都是唯一的。这样就导致构造函数在执行一次就创建一个新的方法。
   3. “解决的方法”：将要创建的对象的内部方法，明在构造函数作用域的外部，全局作用域中。
   4. 但是将函数 在全局作用域内创建，污染了全局作用域的命名空间。并且定义在全局作用域中也很不安全。如何解决这个问题呢？下面提出原型这个概念。

### 原型 | prototype

* 我们创建的每一个函数，解析器都会向函数中添加一个属性 <b>prototype</b> ，这个属性对应着一个对象，这个对象被称为 原型对象。
* 当函数作为普通函数被调用时， prototype 无任何作用。
* 当函数作为构造函数被创建时，创建的对象中都会有一个隐含的属性，该属性指向构造函数的原型对象。通过<code>__ proto __</code>来访问该属性。
* ![image](https://github.com/jiuice/JavaScript-/blob/main/images/image-20201227162804964.png)


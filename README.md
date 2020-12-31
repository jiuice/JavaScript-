### 对象的概念

##### 			          对象分为:内建对象、宿主对象、自定义对象。

* 内建对象： 由ECMAScript实现提供的，独立与宿主环境的所有对象，在ECMAScript程序开始执行时出现。这意味着开发者不必明确实例化内置对象，它已经被实例化了。ECMA只定义了两个内置对象，即Global和Math（它们也是本地对象，根据定义，所有内置对象都是本地对象）。
* 宿主对象：所有非本地的对象都是宿主对象。即，由ECMAScript实现的宿主环境提供的对象。例：所有的BOM、DOM对象都是宿主对象
* 自定义对象：用于自己定义的对象就是自定义对象。

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
* ![image-20201227162804964](C:\Users\穆秋实\AppData\Roaming\Typora\typora-user-images\image-20201227162804964.png)
* 原型对象的作用：其相当于一个公共区域，所有的同一个类的实例都可以访问到这个原型变量。我们可以将对象中共有的内容，统一设置到原型对象中。
* ![image-20201227165551371](C:\Users\穆秋实\AppData\Roaming\Typora\typora-user-images\image-20201227165551371.png)
* 当我们访问对象中的一个属性或方法时，他会先在自生对象中寻找，如果找到直接使用。如果未找到，则到原型对象中寻找，找到直接使用。未找到就是未定义。
* 向构造方法的原型中添加一个属性时，当使用 in 检查实例化对象中是否含有某个属性时。若对象中没有，原型中有，则返回true。
* 对于只判断当前对象中是否存在该属性，请使用 hasOwnProperty("属性名");只有当前对象自身中含有属性时，返回true。
* 关于 hasOwnProperty(); 方法存在哪里？注意原型对象也是对象，该方法在原型对象的对象中。属性或方法的使用规则是：自身中如果有，直接使用。如果自身中没有去原型中寻找，找到则使用。若原型中还没有，则去原型的原型中寻找，找到即用。根据此特性，可以重写系统方法，定制化开发。

### 垃圾回收（GC）

* ##### 当一个对象没有任何的变量或属性，对它进行引用时此时我们将永远无法使用该对象。此时该对象还占用内存空间，就变成了垃圾。

* JS拥有自动的垃圾回收机制，会自动将这些垃圾对象销毁。

* 我们需要做的是，将不再使用的对象设置为 null 即可。

### 数组对象

* 创建：

  1. 使用字面量创建数组：var arr = [元素1，元素2，元素3];
  2. new 关键字创建数组：var arr = new Array(元素1，元素2，元素3); 当传一个参数时是数组的长度值。

* 添加元素：arr[0] = xxx; arr[1] = xxx; .......

* 读取元素：arr[索引]； 数组[索引] 访问元素，索引不存在，不报错，返回undefined。

* 数组名.length 获取到数组的最大索引+1.

  1. 修改 length的值大于原长度，则多余的部分会空出来。

  2. 修改 length的值小于原长度，则多余元素会被删除。
  3. arr[arr.length]索引的位置是数组的最后。

  ##### 数组的方法：

  * push(): 该方法可以向数组的末尾添加一个或多个元素，并返回数据的新的长度。可将要添加的元素作为方法的参数传递。arr.push("xxx");
  * 

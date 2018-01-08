### 介绍Scala中的各个奇技淫巧

* **面向表达式编程**
在Scala中，任何代码块、函数、对象除非显示指明无返回值，否则都是会生成计算结果的。如：
val tmp=for (i <- 1 to 3) yield i     //Seq(1,2,3)
def relu(x:Double)=if(x<0) 0.0 else x  

* **函数式编程**
将函数作为第一类对象（和普通的数据类型、对象一样可以赋值、作为参数、当做返回值），支持lambda表达式、惰性计算、闭包、表达式等特性。

* **Scala集合**
（a）Scala实现了两套集合系统（immutable and mutable）immutable 集合在添加删除元素时，生成一个新的集合，原来的集合并未发生变化，而mutable集合是对原有的集合进行操作，并未产生新集合。通过一些函数组合子（Functional Combinators）对集合进行操作。
常见的集合类型包括：
 (1) List构造列表的两个基本单位是 Nil 和 ::，Nil表示为一个空列表。对于List有三个基本操作：（1）head返回列表的第一个元素，（2）tail返回除了第一个元素外的其他元素；（3）isEmpty判断列表是否为空。
 (2) Set元素不重复。
 (3) Tuple元组中可以包含不同类型的元素。
 (4) Map 包含三个基本操作：keys、values、isEmpty
 (5) Option是一个表示有可能包含值得容器，实现了一个基本的接口。
 trait Option[T] {
  def isDefined: Boolean
  def get: T
  def getOrElse(t: T): T
}Option本身是泛型的，并且有两个子类： Some[T] 或 None。
 （b）一些常见的函数组合子(Functional Combinators)包括：
 map/foreach/zip/filter/partition/find/drop/fold/flatMap。用法略

* **Scala类型系统**


* **Future和Promise区别**

所谓Future，是一种用于指代某个尚未就绪的值的对象。而这个值，往往是某个计算过程的结果：

* 若该计算过程尚未完成，我们就说该Future未就位；
* 若该计算过程正常结束，或中途抛出异常，我们就说该Future已就位。

Future的就位分为两种情况：

* 当Future带着某个值就位时，我们就说该Future携带计算结果成功就位。
* 当Future因对应计算过程抛出异常而就绪，我们就说这个Future因该异常而失败。

Promise 承诺返回Future计算的值，允许你在 Future 里放入一个值，不过只能做一次，Future 一旦完成，就不能更改了。


参考资料：https://twitter.github.io/scala_school/zh_cn/index.html



### 介绍Scala中的各个奇技淫巧

* **面向表达式编程**
在Scala中，任何代码块、函数、对象除非显示指明无返回值，否则都是会生成计算结果的。如：
val tmp=for (i <- 1 to 3) yield i     //Seq(1,2,3)
def relu(x:Double)=if(x<0) 0.0 else x  

* **函数式编程**


* **Scala集合**

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



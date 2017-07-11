### Scala语言杂项

- Scala伴生对象中apply和unapply方法

apply方法：在一个类的半生对象中定义apply方法，在生成这个类的对象时，就省去了new关键字。

unapply方法：可以认为unapply方法是apply方法的反向操作，apply方法接受构造参数变成对象，而unapply方法接受一个对象，从中提取值。


```
class Currency(val value: Double, val unit: String) {

}
object Currency{

  def apply(value: Double, unit: String): Currency = new Currency(value, unit)

  def unapply(currency: Currency): Option[(Double, String)] = {
    if (currency == null){
      None
    }
    else{
      Some(currency.value, currency.unit)
    }
  }
}
```


- Scala implicit方法
# Java 克隆

****

### 构造对象的4种方式：

1.  一种是new，通过new关键字在堆中为对象开辟空间，在执行new时，首先会看所要创建的对象的类型，知道了类型，才能知道需 要给这个对象分配多大的内存区域，分配内存后，调用对象的构造函数，填充对象中各个变量的值，将对象初始化，然后通过构造方法返回对象的地址；
2.    另一种是clone，clone也是首先分配内存，这里分配的内存与调用clone方法对象的内存相同，然后将源对象中各个变量的值，填充到新的对象中，填充完成后，clone方法返回一个新的地址，这个新地址的对象与源对象相同，只是地址不同。
3. 另外还有输入输出流

```java
public Object deepClone() throws IOException, OptionalDataException,ClassNotFoundException {
    // 将对象写到流里
    ByteArrayOutputStream bo = new ByteArrayOutputStream();
    ObjectOutputStream oo = new ObjectOutputStream(bo);
    oo.writeObject(this);
    // 从流里读出来
    ByteArrayInputStream bi = new ByteArrayInputStream(bo.toByteArray());
    ObjectInputStream oi = new ObjectInputStream(bi);
    return (oi.readObject());
} 
```

4. 反射构造对象等

   ****
   

   - 实现Cloneable 接口，调用方法Object.clone() 是浅复制，目标对象的基本数据类型的类成员变量，不会影响源对象的属性值，如果成员变量是对象，则目标对象内的成员变量值更改，会影响到源对象的成员变量值，因为彼此都是引用了同一个对象。即当一个对象赋值给另一个对象变量时，是相同的引用，公用这个对象实例；

   - 浅拷贝，需要实现Cloneable这个标记接口，然后自行实现clone方法，clone方法的默认就是浅拷贝；注意：当对象中成员变量都是基本类型或者不可变量如String的时候，浅拷贝是安全的。但是当变量中存在子对象变量的引用时，就需要深拷贝了，因为浅拷贝并不会对子对象进行clone，这样就造成子对象变为共享域，对象和对象副本都会造成它的状态等改变。因此，深拷贝就类似于递归的把对象本身及对象中包含的对象都进行clone。

   - 深拷贝，  深拷贝不仅拷贝对象本身，而且拷贝对象包含的引用指向的所有对象。

```
还有关键的一点：要使用clone关键字，类的成员变量不要加final关键字！！！！！！！！
```
# string 数据结构

源码包 src/runtime/string.go:stringStruct 定义了string的数据结构：

```golang
type stringStruct struct {
	str unsafe.Pointer // 字符串的首地址;
	len int //字符串的长度;
}
```

# string操作

```golang
// 声明变量;
var str string 
str = "Hello World"

// string转[]byte;
b := []byte(str)

// []byte转string;
bStr = string(s)
```

string转换成byte切片，byte切片转string时，都需要一次内存拷贝。

# 为什么字符串不允许修改？

像C++语言中的string，其本身拥有内存空间，修改string是支持的。但Go的实现中，string不包含内存空间，只有一个内存的指针，这样做的好处是string变得非常轻量，可以很方便的进行传递而不用担心内存拷贝。

因为string通常指向字符串字面量，而字符串字面量存储位置是只读段，而不是堆或栈上，所以才有了string不可修改的约定。

# string和[]byte如何取舍

string和[]byte都可以表示字符串，但因数据结构不同，其衍生出来的方法也不同，要跟据实际应用场景来选择。

### string 擅长的场景：

- 需要字符串比较的场景；
- 不需要nil字符串的场景；

### []byte擅长的场景：

- 修改字符串的场景，尤其是修改粒度为1个字节；
- 函数返回值，需要用nil表示含义的场景；
- 需要切片操作的场景；
- 虽然看起来string适用的场景不如[]byte多，但因为string直观，在实际应用中还是大量存在，在偏底层的实现中
- []byte使用更多。
# String
## 类签名
```java
public final class String
    implements java.io.Serializable, Comparable<String>, CharSequence
```
![](../images/String-UML.png)

String 类有 final 修饰
## API
### 变量
```java
private final char value[];
private int hash; // Default to 0

public static final Comparator<String> CASE_INSENSITIVE_ORDER = new CaseInsensitiveComparator();

private static final ObjectStreamField[] serialPersistentFields = new ObjectStreamField[0];
```
- char value[] 
  - char[] 作为String的背后数据结构
- CASE_INSENSITIVE_ORDER
  - 一个由compareToIgnoreCase排序String对象的比较器。该比较器是可序列化。
  - 该比较器未考虑locale环境，会导致某些locale环境的排序不符合期望。java.text包提供了Collators以允许对locale环境敏感的排序。
- serialPersistentFields
  - String 类在序列化流协议中是特殊情况。根据对象序列化规范第6.2节“流元素”，将String实例写入ObjectOutputStream中。
  
### 构造方法
```java
public java.lang.String();
public java.lang.String(java.lang.String);
public java.lang.String(char[]);
public java.lang.String(char[], int, int);
public java.lang.String(int[], int, int);
public java.lang.String(byte[], int, int, int); // @Deprecated
public java.lang.String(byte[], int);// @Deprecated
public java.lang.String(byte[], int, int, java.lang.String) throws java.io.UnsupportedEncodingException;
public java.lang.String(byte[], int, int, java.nio.charset.Charset);
public java.lang.String(byte[], java.lang.String) throws java.io.UnsupportedEncodingException;
public java.lang.String(byte[], java.nio.charset.Charset);
public java.lang.String(byte[], int, int);
public java.lang.String(byte[]);
public java.lang.String(java.lang.StringBuffer);
public java.lang.String(java.lang.StringBuilder);
java.lang.String(char[], boolean);
```
可见有很多String的构造函数。
#### public String()
```java
public String() {
    this.value = "".value;
}
```
""初始化value

#### public String(String original)
```java
public String(String original) {
    this.value = original.value;
    this.hash = original.hash;
}
```
入参为String类型，复制String的value和hash值到内部value。

#### public String(char value[])
```java
public String(char value[]) {
    this.value = Arrays.copyOf(value, value.length);
}
```
入参为char[]类型，使用Arrays.copyOf进行复制。
#### public String(int[] codePoints, int offset, int count)
```java
public String(int[] codePoints, int offset, int count) {
    if (offset < 0) {
        throw new StringIndexOutOfBoundsException(offset);
    }
    if (count <= 0) {
        if (count < 0) {
            throw new StringIndexOutOfBoundsException(count);
        }
        if (offset <= codePoints.length) {
            this.value = "".value;
            return;
        }
    }
    // Note: offset or count might be near -1>>>1.
    if (offset > codePoints.length - count) { // 这样易于理解：offset + count > codePoints.length 
        throw new StringIndexOutOfBoundsException(offset + count);
    }

    final int end = offset + count; // end为终点index，但不包含end

    // Pass 1: Compute precise size of char[]
    int n = count;
    for (int i = offset; i < end; i++) {
        int c = codePoints[i];
        if (Character.isBmpCodePoint(c))
            continue;
        else if (Character.isValidCodePoint(c)) 
            n++;
        else throw new IllegalArgumentException(Integer.toString(c));
    }

    // Pass 2: Allocate and fill in char[]
    final char[] v = new char[n];

    for (int i = offset, j = 0; i < end; i++, j++) {
        int c = codePoints[i];
        if (Character.isBmpCodePoint(c))
            v[j] = (char)c;
        else
            Character.toSurrogates(c, v, j++);
    }

    this.value = v;
}
```
- 作用：分配一个新的String，该字符串包含Unicode code points数组参数的子数组中的字符。
- 入参说明
  - codePoints - Unicode code points 源数组
  - offset - 偏移量，复制的开始位置
  - count - 复制长度
- 代码解析
```java
// Pass 1: Compute precise size of char[]
int n = count;
for (int i = offset; i < end; i++) {
    int c = codePoints[i];
    if (Character.isBmpCodePoint(c))
        continue;
    else if (Character.isValidCodePoint(c)) 
        n++;
    else throw new IllegalArgumentException(Integer.toString(c));
}
```
> 区分 BmpCodePoint 和 ValidCodePoint

如果指定的字符在基本多语言平面BMP中，可使用单个char表示这个代码点。ValidCodePoint 指 Unicode code point value。
n初始值为入参count，上面代码在遇到code point等于ValidCodePoint时，将n++。最终n等于char[]的实际长度。

```java
// Pass 2: Allocate and fill in char[]
final char[] v = new char[n];

for (int i = offset, j = 0; i < end; i++, j++) {
    int c = codePoints[i];
    if (Character.isBmpCodePoint(c))
        v[j] = (char)c;
    else
        Character.toSurrogates(c, v, j++);
}
```
开辟精确长度的新的char[]后，开始遍历
- 如果code point为BMP，那么直接转为char，然后赋值
- 如果不为BMP，那么调用 Character.toSurrogates(c, v, j++)
```java
static void toSurrogates(int codePoint, char[] dst, int index) {
    // We write elements "backwards" to guarantee all-or-nothing
    dst[index+1] = lowSurrogate(codePoint);
    dst[index] = highSurrogate(codePoint);
}
```

#### StringCoding.decode(charsetName, bytes, offset, length)
```java
public java.lang.String(byte[], int, int, java.lang.String) throws java.io.UnsupportedEncodingException;
public java.lang.String(byte[], int, int, java.nio.charset.Charset);
public java.lang.String(byte[], java.lang.String) throws java.io.UnsupportedEncodingException;
public java.lang.String(byte[], java.nio.charset.Charset);
public java.lang.String(byte[], int, int);
public java.lang.String(byte[]);
```
上面这些以byte[]为第一个入参的方法都会调用 StringCoding.decode(charsetName, bytes, offset, length)。

#### public String(StringBuffer buffer)
```java
public String(StringBuffer buffer) {
    synchronized(buffer) {
        this.value = Arrays.copyOf(buffer.getValue(), buffer.length());
    }
}
```
这里为什么对入参buffer加了同步 synchronized ？

#### public String(StringBuilder builder)
```java
public String(StringBuilder builder) {
    this.value = Arrays.copyOf(builder.getValue(), builder.length());
}
```
提供此构造函数是为了简化StringBuilder迁移到String。从string builder通过toString方法获取字符串可能会运行得更快，通常是首选。

### int length()
```java
public int length() {
    return value.length;
}
```

### boolean isEmpty()
```java
public boolean isEmpty() {
    return value.length == 0;
}
```
### char charAt(int index)
```java
public char charAt(int index) {
    if ((index < 0) || (index >= value.length)) {
        throw new StringIndexOutOfBoundsException(index);
    }
    return value[index];
}
```
> 如果index指定的char值是surrogate，则返回该surrogate值。

### int codePointAt(int index)
```java
public int codePointAt(int index) {
    if ((index < 0) || (index >= value.length)) {
        throw new StringIndexOutOfBoundsException(index);
    }
    return Character.codePointAtImpl(value, index, value.length);
}
```
暂停，回去看 Character

## Surrogate
> TODO 

## 说明
- String 是常量，值创建后无法更改，可以共享。StringBuffer支持可变字符串。
- 除非另有说明，将null参数传递给此类中的构造函数或方法将导致引发NullPointerException。
- 一个 String 表示UTF-16格式的字符串，其中补充字符由surrogate pairs表示（参见Character类中的Unicode字符表示部分）。 
索引值是指char code单位，一个补充字符在String中使用两个position。
- 除了提供处理Unicode代码单元（即char）的方法外，还提供用于处理Unicode代码点（即characters）的方法。


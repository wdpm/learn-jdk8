# Learn JDK 8
学习 JDK 8 源码设计。

## 阅读前的准备
下载 jdk1.8.0_211，将其中的 src.zip 文件解压。解压后目录如下(部分已省略)：
```
└─src
    └─java
        ├─io
        ├─lang
        ├─math
        ├─net
        ├─nio
        ├─security
        ├─sql
        ├─text
        ├─time
        └─util
```

## 阅读工具
- Intellij IDEA
  - Structure View：用于查看类的方法签名
  - Diagrams -> Show Diagrams 用于查看类的继承结构
- CopyTranslator：用于复制英文注释进行翻译，快速查词
- Configure [J2SE 8 API docs](https://docs.oracle.com/javase/8/docs/api/) in Intellij IDEA Documentation Path

## 阅读方法
- 从具体的实现类找到最顶层父类/父接口，然后自顶向下查看实现。
- 首先看类注释说明，这个描述具有高度的概括性，利于大体上理解。
- 其次看某些方法的注释，一般是这个方法的概括说明。
- 最后看方法里面的零碎注释，跳过实在难以理解的地方，例如Hacker delight。
 
## 阅读计划
- java.lang
  - [x] Object
  - [x] CharSequence
  - String
  - AbstractStringBuilder
  - StringBuffer
  - StringBuilder
  - [x] Boolean
  - [x] Byte
  - [x] Short
  - [x] Integer
  - [x] Long
  - Float
  - [x] Double
  - Thread
  - ThreadLocal
  - Enum
  - Throwable
  - Error
  - Exception
  - Class
  - ClassLoader
  - Compiler
  - System
  - Package
  - Void
    
- java.util
  - [x] Iterable
  - [x] List
  - [x] Collection
  - [x] AbstractCollection
  - [x] ListIterator
  - [x] RandomAccess
  - [x] Serializable
  - [x] Cloneable
  - [x] AbstractList
  - AbstractMap
  - AbstractSet
  - [x] ArrayList
  - LinkedList
  - HashMap
  - HashTable
  - BitSet
  - HashSet
  - LinkedHashMap
  - LinkerHashSet
  - TreeMap
  - TreeSet
  - Vector
  - Queue
  - Stack
  - SortedMap
  - SortedSet
  - Collections
  - Arrays
  - Comparator
  - Iterator
  - Base64
  - Date
  - EventListener
  - Random
  - SubList
  - Timer
  - UUID
  - WeakHashMap
  
- java.util.function
  - [x] Consumer
  - [x] UnaryOperator
  
- java.util.concurrent
  - ConcurrentHashMap
  - Executor
  - AbstractExecutorService
  - ExecutorService
  - ThreadPoolExecutor
  - BlockingQueue
  - AbstractQueuedSynchronizer
  - CountDownLatch
  - FutureTask
  - Semaphore
  - CyclicBarrier
  - CopyOnWriteArrayList
  - SynchronousQueue
  - BlockingQueue
  - Callable
  
- java.util.concurrent.atomic
  - AtomicBoolean
  - AtomicInteger
  - AtomicLong
  - AtomicReference
- java.lang.reflect
  - Field
  - Method
 
- java.lang.annotation
  - Annotation
  - Target
  - Inherited
  - Retention
  - Documented
  - ElementType
  - Native
  - Repeatable
  
- java.util.concurrent.lock
  - Lock
  - Condition
  - ReentrantLock
  - ReentrantReadWriteLock
  
- java.io
  - File
  - InputStream
  - OutputStream
  - Reader
  - Writer
  
- java.nio
  - Buffer
  - ByteBuffer
  - CharBuffer
  - DoubleBuffer
  - FloatBuffer
  - IntBuffer
  - LongBuffer
  - ShortBuffer
  
- java.sql
  - Connection
  - Driver
  - DriverManager
  - JDBCType
  - ResultSet
  - Statement
  
- java.net
  - Socket
  - ServerSocket
  - URI
  - URL
  - URLEncoder

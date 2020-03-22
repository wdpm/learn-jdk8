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
  - Structure feature
  - Diagrams -> Show Diagrams
 
## 阅读计划
- java.lang
  - Object
  - String
  - AbstractStringBuilder
  - StringBuffer
  - StringBuilder
  - Boolean
  - Byte
  - Double
  - Float
  - Integer
  - Long
  - Short
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
  - AbstractList
  - AbstractMap
  - AbstractSet
  - ArrayList
  - LinkedList
  - HashMap
  - HashTable
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

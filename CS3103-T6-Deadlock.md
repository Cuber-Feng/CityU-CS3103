# 🧵Deadlock

## 🔍Reasons of Deadlock

### Reason 1

- In large code bases, complex dependencies arise between components

- 大型代码库中组件依赖复杂, 如果多个组件相互依赖，并且同时尝试访问共享资源，就容易出现**互相等待资源**的情况，从而引发死锁

### Reason 2

- 封装（**Encapsulation**）与加锁机制的不兼容

- 面向对象编程中常用“封装”来隐藏模块内部实现，让代码更模块化、易维护。

- 但问题是：加锁机制需要开发者了解哪些资源会被访问（比如哪些锁会被获取）。

- 如果封装隐藏了这些细节，你无法知道某个模块内部是否加了锁，也无法保证你使用多个模块时的加锁顺序是一致的。

- 这样就很容易造成多个模块之间的锁顺序不一致 → 产生死锁。

## 🪂Conditional for Deadlock 缺一不可

### 1. Mutual Exclusion

- 线程要对其所需资源单独占有
- 改进代码, 不要写锁
- CompareAndSwap

### 2. Hold-and-wait

- 拿着一个等另一个
- 让对多个锁的申请原子化, 申请几个锁的中途不能有别的线程插入
- 坏处: 破坏并发(concurrency)

### 3. No preemption

- 不能把资源从别的thread那里抢过来

#### trylock

- 按顺序获取锁, 如果空闲就持有, 如果不空闲就放弃前面获得的所有锁, 重新来一遍

#### livelock

- 每次重新开始一次循环的时候等待随机时间

### 4. Circular Wait

- 存在一个循环的线程链，每个线程都持有一个及以上的资源，这些资源正被链中的下一个线程请求

- 给资源设定顺序

- 比如有L1&L2, 规定必须先申请L1, 再申请L2

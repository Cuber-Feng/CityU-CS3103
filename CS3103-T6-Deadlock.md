# 🧵Deadlock
> Last updated: Apr 12, 2025
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

## 👌Deadlock Avoidance 主动避免死锁
- 需要额外的信息来储存 how resources are to be requested
- 每个 process declares 它需要的最大资源数量
- Deadlock-avoidance algorithm 确保永远没有 circular-wait condition
- 资源分配状态 Resource-allocation state：
  - 可用资源的数量和已分配资源的数量(available and allocated)
  - 进程的最大需求
### Safe State
- 系统是否“安全” = 是否有一个“顺序”，能让所有进程一个个完成并释放资源。
- 不安全不代表一定死锁
- Deadlock avoidance: ensure a system never enters an unsafe state
### Deadlock Avoidance Algorithms
#### Resource-Allocation Graph (每本书只有一份)
- 两种节点
  - process
  - resource type
- 两种边(有向)
  - request edge: 从进程指向资源
  - assignment edge: 从资源指向进程
  - claim edge: 从进程指向资源(进程可能请求某个资源, 虚线)
- Transitions in between edges
  - claim edge --> request edge: when a process requests resource
  - request edge --> assignment edge: when resource allocated to process
  - assignment edge --> claim edge: when resource released by process
- **没有圈就是安全状态**(有向圈)
  - 如果一个 request edge 变成 assignment edge 后不会形成新的圈, 则这个 request 可以通过
#### Banker’s Algorithm (每本书有多份)
- 前提
  - 每个进程必须事先声明它对每种资源类型的**最大需求量**
  - 当进程请求资源时，可能要等待
  - 当进程获得它需要的所有资源后，必须在**有限时间**内释放资源

- 术语

|名称 |	含义|
|--|--|
|Available	|系统当前可用的各类资源数量|
|Max	|每个进程最大可能需要的资源量|
|Allocation	|当前已分配给每个进程的资源量|
|Need	|每个进程还需要的资源量（Need = Max - Allocation）|

具体过程比较复杂, 看这个吧: [Banker's Algorithm explained](https://youtu.be/T0FXvTHcYi4?si=wVo7jk7OCICI_dRA)

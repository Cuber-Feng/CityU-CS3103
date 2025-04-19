# Group Project A
## 作业目标:
- 学习如何使用 POSIX 信号量**同步**进程的执行并协调 **共享内存段(shared
 memory segment)** 的使用。
- 学习如何使用 POSIX 线程协调多线程编程中多个线程的执行。
- 学习理解文件系统以及相关的目录/文件操作。
## 提供的文件:
```python
 Project
 |-- test_case/ # The test case directory for problem 2.
 |-- helpers.c # Useful functions
 |-- helpers.h # Useful functions
 |-- problem1.c # The source code file for problem 1.
 |-- problem2.c # The source code file for problem 2.
 ‘-- Makefile # It can be used to compile source code.
```
- helper.h 里有一些函数, helper.c里用到了, 请理解这些函数, 并使用
- Makefile 可以直接给problem1.c编译, 也可以修改它来编译其他的c语言程序
- problem1.c 里有一些sample code, 关于怎么创建process, 使用共享内存, 信号量.
- problem2.c 里提供了problem 2 的一些必要的逻辑.
## 参考
- [Shared Memory](https://man7.org/linux/man-pages/man7/shm_overview.7.html)
- [Semaphore](https://man7.org/linux/man-pages/man7/sem_overview.7.html)
- 函数:

| Function          | Description                                  |
|-------------------|----------------------------------------------|
| shmget()         | Allocate a shared memory segment            |
| shmat()          | Shared memory attach operation              |
| shmdt()          | Shared memory detach operation              |
| shmctl()         | Perform the control operation for a shared memory |
| sem_open()       | Initialize and open a named semaphore       |
| sem_init()       | Initialize an unnamed semaphore             |
| sem_wait()       | Lock a semaphore                            |
| sem_post()       | Unlock a semaphore (similar to signal() in lecture) |
| sem.close()      | Close a named semaphore                     |
| sem_unlink()     | Remove a named semaphore                    |
| sem_destroy()    | Destroy an unnamed semaphore                |
| pthread_create() | Create a new thread                         |
| pthread_join()   | Join with a terminated thread               |
| pthread_exit()   | Terminate the calling thread                |
## 具体要做什么:
实现两个C语言程序, 先做Problem 1再做Problem 2
### Problem 1
#### Intro
问题 1 旨在帮助你理解进程（或线程）之间如何使用共享内存和信号量。请实现你的程序（problem1.c），运行它并回答关于问题 1 的问题。

我们使用 fork() 系统调用创建一个新的子进程。之后，父进程和子进程将独立并发地执行各自的代码。父进程从终端的命令行中获取一个输入参数（参见下面的"如何运行问题1"）。输入参数应该是您小组成员的城大学号之一(8位整数)。然后，父进程将输入参数的值赋给三个变量。子进程尝试通过读取这些变量的值并将其打印到终端来获取输入参数。我们使用信号量 PARAM ACCESS SEMAPHORE 来协调进程之间对变量的操作。这样，我们可以确保任何时候只有一个进程可以访问这些变量，即互斥。

#### 如何运行问题1
```
$ make 或者 $ gcc problem1.c helper.c-o problem1-I.-pthread
$ ./problem1 <input_param>
```
#### Question 1

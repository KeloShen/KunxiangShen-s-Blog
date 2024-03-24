---
title: "OS: Some questions and answeres in my learning period"
datePublished: Sun Mar 24 2024 09:04:40 GMT+0000 (Coordinated Universal Time)
cuid: clu5am8pf000009ktddjge2ck
slug: os-some-questions-and-answeres-in-my-learning-period
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/z508Zk08HNU/upload/4e12ca94a860329a56d3685b71b4d90d.jpeg
tags: operating-system, study, thinking

---

## Theory Learning

### Semaphores & Atomic Operations

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711265512556/8562d65a-629b-477a-b674-5ddf887adfbc.png align="center")

如图所示，在学习信号量实现的过程中，老师举了一个例子，有A、B、C、D四个进程，其分别进行PV操作，观察变化，我注意到第5号操作，轮到C进程要开始进行P操作的时候，因为s的值为0，所以其会进行空转，D也是如此，然后老师说会跳到B再进行V操作。这个时候我的疑惑就来了，原子操作是不可以被中断的，而上一个P操作一直在进行空转，没有结束，为什么可以轮到另外一个进程再进行操作？

经过查询，我发现我自己对前面所学的知识有一些误区以及掌握不牢固。我需要先把这个过程阐述明确。

首先，轮到5号操作，此时s==0，再进行调度C进程的时候，通过检测后进行空转，而空转会引起操作系统的挂起，即将C进程的状态由running切换为blocked（or waiting），此时进行下一步操作，CPU调度D进程，而D进程同理，再进行下一步，调度B操作，B操作结束后s==1，再进行调度C程序，此时进行检测后发现资源可以使用，唤醒处于blocked状态的C进程，切换为ready状态，然后进行running，继续进行P操作，s信号量减1，此时s==0，再进行V操作，s==1。

而我的误区在于，running切换到blocked的过程，我认为属于中断，所以我比较疑惑为什么处于原子操作P这下还可以这样进行调度。

1.由running切换为blocked状态的过程不属于中断，它可能是由于进程主动请求某些资源（如等待 I/O 完成）或者由于某些条件尚未满足而暂停执行的。调度器会根据一定的策略选择另一个进程来运行，这个过程通常不会被称为中断。

2.由C进程切换到另外一个进程的过程（调度器在选择新的进程运行时）可能会根据某些条件（如进程的优先级、等待时间等）进行评估，而某些情况下可能会表现得类似于中断处理程序的行为。但从操作系统的角度来看，这个过程通常更像是操作系统的内部机制，而不是严格意义上的中断处理。

又引出来一个问题，进程切换的过程中必须有中断吗？什么样的进程切换可以称之为中断？
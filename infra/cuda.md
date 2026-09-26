## 术语

- prefill：将输入的的整段prompt都喂给模型，计算对应的kv cache

## prefix cache

每一个块都会计算一个hash，如果一个块有前缀，会在计算的时候加上块的前缀块

比如块A={1,2,3,4}  H1 = hash(A).  B = {2,3,4,5} H2 = {H1 + B)

因为kv cache是上下文相关的，所以block也是上下文相关的

# gpu

关键词

## **_shared__ to declare a array in shared memory**

## execution barrier

_syncthreads(). 同一个块内的所有的线程都必须达到这个语句之后，才可以执行后面的代码

常见模式，共同加载共享内存，在一个非条件语句中放置同步线程模型，确保所有的数据都ready

## dram shared-memory
当用到一个字节的时候，dram会发送32个字节，占用32个字节的传输带宽
access dram by segment not by byte
共享内存不需要连续的内存访问

## gpu 架构
* 双发射：一个wrap scheduler在一个时钟周期内部从同一个指令流中连续发出两条相邻的指令
* software model: 基础单元是线程，这些线程被组织成线程块，线程块有组织成了grid 
grid是一次内核启动所有的线程块的集合
* wrap：一个线程束由32个线程组成 一般情况下以wrap为单位执行指令，



![alt text](image.png)
1. 线程被scalar processor处理的，也就是cuda core/sp，
2. 线程块被sm处理
3. 一个thread block一旦被一个sm占用，就不会更换
4. 一个sm可以驻留多个core，但是最后不会进行

## cuda configuration
1. 单个线程内部的指令还是按照顺序发射执行的。
2. 当一条指令需要的数据没有准备好，会stall(停顿)
Memory read by itself doesn't stall execution 在读内存的时候gpu会调度其他的线程，所以 GPU 用大量线程隐藏内存延迟。这就是Latency hiding（延迟隐藏）
3. Latency is hidden by switching threads 读取global memory需要>100cycle,计算<100cycles

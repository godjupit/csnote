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
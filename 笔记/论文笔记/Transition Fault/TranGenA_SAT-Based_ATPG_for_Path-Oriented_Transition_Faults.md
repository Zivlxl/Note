# TranGen: A SAT-Based ATPG **for** **Path-Oriented Transition Faults**

通常情况下，对于gate delay模型，一般默认有假设：故障效应足够大以至能被检测到。对于小型（small-size）延时缺陷，path delay模型效果更好，但是电路中可能有指数级个敏化路径，一般只选择部分关键路径（timing critical paths)。



gate delay模型 **VS **path delay模型

门延时模型的优势在于有完整的拓扑覆盖率，而路径延时模型可以专注于最糟糕的路径情况



为了检测出small-size和large-size的延时缺陷，通常选择将两种延时模型组合起来。该文章即是这种思路，提出了一种path-orientned transition fault模型，在这个模型中，假设所有的跳变故障都可以通过最长的敏化路径检测出来。同时，该文章使用SAT求解器进行测试生成（通过错误路径裁剪技术（false-path pruning），SAT solver容易使用），生成的测试集效果比起组合两种延时模型的要好。

不过问题在于，这种混合模型是path-oriented，通常一个故障的测试向量不太可能检测出其他地方的跳变故障，导致所需的test pattern集比较大，也就是说，这种方法获得的故障集一个test pattern往往只能检测一个fault








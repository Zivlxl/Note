# Efficient Techniques for Transition Testing

基于扫描的跳变测试往往要求大量的时间和测试生成，本文提出了一种结合跳变测试链和ATE重复能力的方法，用于减少测试生成数据，但这往往不能带来的测试时间的减少。在此基础上，又提出了一种叫做交换扫描的新方法。同时本文还旨在处理由于不可测试跳变故障导致的常量降低问题（又称为overtesting）。



延迟模型有三种：transition fault、path delay fault、segment delay fault



跳变测试有三中实现方式：

- Broadside
- Skewed-Load
- Enhanced-scan：两个测试向量`(v1, v2)`都存在扫描存储器中。第一次扫描移位将`v1`加载到扫描链中，接着将这个扫描链应用到在测电路上。下一步，将`v2`扫描进去，并且应用到电路上，之后捕获结果。在这个过程中，需要保证的是输入`v2`时，不能改变电路由`v1`带来的状态。基于上面的认识，需要由hold-scan设计，这便是Enhance-scan测试的缺点。



##### ATE模型

![image-20220618101737093](C:\Users\ziv\AppData\Roaming\Typora\typora-user-images\image-20220618101737093.png)

每个通道有3个比特串，分别是test pattern，response和mask，mask有U（不掩盖响应）和M（掩盖响应）。





##### Exchange scan

![image-20220618154917539](C:\Users\ziv\AppData\Roaming\Typora\typora-user-images\image-20220618154917539.png)

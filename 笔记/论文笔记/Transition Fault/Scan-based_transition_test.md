# Scan-based Transition Test

#### delay test

delay test又称AC test



delay fault model

- gate delay



- path delay



如果在实践中，如果出现的缺陷经常是点部（局部）缺陷，经常使用gate delay故障模型；但是，如果缺陷的性质更全局，则有必要采用路径延迟故障模型。另外，从测试向量生成、故障模拟、故障诊断等角度来看，gate delay故障模型复杂度更小。



不同于sa故障，等到输出信号稳定时就可检测到故障；delay fault要满足特定的条件下（certain conditions）才能有效。同时，在考虑故障覆盖率时，也得考虑这些条件。

对于delay fault，主要有两个担忧：1、hazard的出现可能会影响delay test，即有问题时仍然通过测试；2、故障效应可能会被电路中的其他部分覆盖掉。

robust test：确保延迟测试是有效的，而不管在逻辑电路的其他部分的延迟的测试，可以出现hazard，只要其不影响测试

Hazard-free tests：是稳健测试的一个子集，它们排除了用于传播故障效应的信号值中存在的hazard

delay test所需的测试向量集是其对应sa故障所需向量集的超集



跳变测试VS健壮测试：跳变测试不需要最终的输出要和初始状态下的输出（initial state）相同，只要在施加final pattern之后，到其输出稳定之前，有互补的输出能检测出故障即可；而健壮测试所需的final pattern一定要最终的稳定输出和初始输出相反

有两种scan-based transition test

- broad-side transition test 需要两个扫描链，不用考虑移位依赖（shift dependency）问题，但是时间框架问题比较复杂
- skew-load transition test （SLOTT） 一个扫描链，有shift denpendence问题，不过时序比较简单



####  SKEWED-LOAD TRANSITION TEST CALCUL

提出了一种基于布尔差分的微积分（Boolean-difference based calculus），能够同时的计算测试向量V1和V2，称为**single time-frame  calculus**。



#### 跳变故障的检测概率






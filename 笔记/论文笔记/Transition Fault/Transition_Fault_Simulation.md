# Transition Fault Simulation



#### 跳变故障模型

- slow to rise 在未跳变之前相当于sa-0
- slow to fall 在未跳变之前相当于sa-1



需要两个test pattern，分别是initialization和transition propagation



#### 故障列表生成

要生成用于故障模拟的列表，跳变故障和sa故障不太一样。对于sa故障，等价故障组中的故障可以使用同一个test pattern测试。而对于跳变故障，故障等价条件不同于sa故障。

只有满足以下两个条件时，才能认为两个故障时等价的：

- 某个门只有一个输入，则可以认为跳变故障（输入和输出端的）等价
- 某个门只有一个扇出，那么在扇出门上，输入跳变和输出跳变是等价的

因为等价条件更为严格，跳变故障等价类的数目要比sa故障大50%左右



#### 模拟策略

跳变故障被检测出的方式：在故障点发生跳变，同时，在一定时间限制内，检测到对应的sa故障



#### LSSD扩展

使用LSSD扫描链






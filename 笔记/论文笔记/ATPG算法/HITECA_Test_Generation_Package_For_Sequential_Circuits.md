## HITEC: A TEST GENERATION PACKAGE FOR SEQUENTIAL CIRCUIT

这篇文章提出的HITEC 算法就是最出名的前向传播故障（Fault Propagation），后向判别状态（Justify）。不同于BACK算法的初始选定一个输出，从该输出开始全部反向判别。



一些概念：

dominator：如果通过某条线（line）l的路径到达任何输出都需要经过门（Gate）g，则g是l的dominator。dominator可以用来寻找强制赋值（mandatory assignment），例如，与门和与非门的所有值都要被设置成非控制值。




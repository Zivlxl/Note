### FAN算法

为了加速PODEM算法，在下面两个方面进行提升：

1. 减少backtrack的次数
2. 减少backtrack发生时耗费的时间

FAN算法和PODEM算法最大的区别就在于FAN算法backtrace不在primary input停止，而是在fan-out point 和head line停止，一般情况下可以减少decision tree的大小

#### 定义

##### backtrack

在decision tree中，某个assignment导致了冲突，回退尝试其他的assignment

##### backtrace

由某些已知的信号值分配，推导出电路中其他的line的信号值，直至发生冲突或到达primary input/output

##### implication

蕴含，指由特定的信号值推测或假设出其他信号线的值

##### unjustified line

门G的输出值确定，但是输出不确定，这种门的输出叫做unjustified line

##### bound、head、free line

如果存在一条通路从fan-out到signal line L，称L为bound

signal line L与一条bound相邻，称L为head line

其他的称为free 

#### 方法

- 如果目标可以通过设置一个输入值来达到（0 for AND, 1 for OR），设置最容易设置的那个输入
- 如果目标需要设置所有的输入值才能达到（1 for AND，0 for OR），设置最难的那个输入，因为可以避免多余的时间消耗在其他门的输入值确定
- 在D-frontier中选择最靠近primary output的门
- 尽可能多的给出唯一的蕴含
- 如果只有一个D-frontier，使用唯一敏化方法（unique sensitization）
- backtrace在head line出结束，而不是知道primary input，因为free line的backtrace不可能由backtrack
- Multiple backtrace，同时backtrace多条路径
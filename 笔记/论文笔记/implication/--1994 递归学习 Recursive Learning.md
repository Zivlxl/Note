## --1994 递归学习 Recursive Learning

递归学习目的是要找到电路中所有“必要”的逻辑值分配，以便在test generation时没有回溯。之前的paper中提出的方法只能检测出部分的necessary assignment，因为它们的时间复杂度是多项式时间，然而该问题是NP-complete问题，只有指数级算法才能找出所有的necessary assignment。


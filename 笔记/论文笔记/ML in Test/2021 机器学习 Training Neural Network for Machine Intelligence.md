## Training Neural Network for Machine Intelligence in Automatic Test Pattern Generator

#### ANN结构

![image-20220302140933030](C:\Users\ziv\AppData\Roaming\Typora\typora-user-images\image-20220302140933030.png)

激活函数：sigmiod函数

输入（特征）：ATPG过程中跟踪电线（trace line）驱动的门类型（被赋予成特定的编码，即one-hot（[0,0,0,…,1,0]这样的编码方式））；CC1，CO，COP；跟踪电线和PIs的最小距离

输出（标签）：如果它属于一个可以生成测试Pattern的backtrace，为1；如果导致了backtrack，为0

误差：均方误差（MSE）

#### 原ANN

![image-20220302140747565](C:\Users\ziv\AppData\Roaming\Typora\typora-user-images\image-20220302140747565.png)

从之前的数据知，在小型电路中，ANN（ANN-guild PODEM）回溯的次数小于使用COP或者distance作为Testability的启发式算法，但是在较大的电路中，ANN回溯的次数是要大于另外两种情形的。

作者认为纠正这些“异常值”需要在以下几个方面对ANN进行i调整：

- 训练电路的选择，使用之前采用的所有电路重新训练ANN
- 训练数据模式之间冲突的解决
- 错误类型的选择。通过调整隐藏层来保持训练误差的减小（固定数量的隐藏层神经元不足以吸收增长的数据量）；只有当训练误差减少时的训练数据（training data for a fault）才被接受；不仅仅使用”难以检测（hard-to-detect）“的故障来生成训练数据
- Forgetfulness（本文未用到）

#### 本文提出的训练方法

##### 解决训练数据间的冲突

在训练数据中，有一些pattern相同，但是标签不同的数据，即{xi}={xj}, zi!=zj。这样的数据会导致MSE不减。解决方法时将这种pattern相同的训练数据分成一组，用一个训练数据代替这一组数据，令lable=count（0）/（count（0）+count（1））。如下图所示，前三个训练数据的pattern相同，完善后的训练数据如第二个图所示。

![image-20220302143652174](C:\Users\ziv\AppData\Roaming\Typora\typora-user-images\image-20220302143652174.png)

##### 递归训练和ANN优化

之前的实验中，使用的训练数据是由使用随机启发式方法的PODEM生成的，这种方法不仅时间长，复杂，同时也难以再现（non-repeatable）。本文的实验训练数据是由以COP为指导的PODEM生成的。

ANN的训练质量与其结构和复杂度有着极大的联系，通过添加或减少隐藏层的神经元确定使得MSE最小的ANN结构。同时使用训练数据多次训练ANN也能减小MSE。

##### 算法

![image-20220302145823547](C:\Users\ziv\AppData\Roaming\Typora\typora-user-images\image-20220302145823547.png)

#### 实验结果

![image-20220302150644451](C:\Users\ziv\AppData\Roaming\Typora\typora-user-images\image-20220302150644451.png)

1. 一些电路如C17、B02、B01等没有reconvergent扇出的电路没有Backtrack。一些其他由reconvergent输出的电路也没有Backtrack。
2. 除了图中未加黑的电路，整体表现优于原ANN。
3. 部分电路CPU运行时间增加。
4. 除了c432电路（基于距离的启发式），表现均比传统启发式方法好。
5. 深度较大的电路CPU运行时间减少的多。

##### 期望

期望：

- 可以将SCOAP考虑进去。
- backtrace增加了。
- 最优的ANN结构可能还需考虑CPU时间。
- 应当尽早发现不可测故障和冗余故障。
- 训练数据的生成。任意的电路可以生成无限的训练数据。

优点：考虑了easy-to-test故障。

问题：

实际中，可以用组合多种ATPG方法，例如使用其他方法生成简单故障的test pattern，使用ANN-based ATPG生成复杂故障的test pattern。

寻找最佳训练电路。

CPU运行时间（尽管训练ANN花费时间很长（一劳永逸），再使用ANN时间则用时相对较少，但这个时间也需进一步优化），例如通过查表减少。
## --2021 综述 Machine Learning in Test

#### 介绍

- 模拟（Analog）和射频（RF）测试是功能化，基于高级规范设计的
- 数字电路测试（digital）是结构化，基于目标错误设计的
- 存储器测试（memory）也是基于目标错误设计的，但是是功能化的方法进行测试

#### 模拟、射频测试

##### 带神经网络的BIST硬件实现

<img src="C:\Users\ziv\AppData\Roaming\Typora\typora-user-images\image-20220301121536943.png" alt="image-20220301121536943" style="zoom:%;" />

<center style="color:#C0C0C0;text-decoration:underline">BIST</center>

Note:

- 人工神经网络训练是通过测量制造芯片的模式并将其映射到一位输出来进行的(off-line)
- 测量采集传感器（Measurement Acquisition Sensor）监控DUT的输出，并且将输出提供给神经网络分类器
- 神经网络下载存储在板上的权重

![image-20220301153225317](C:\Users\ziv\AppData\Roaming\Typora\typora-user-images\image-20220301153225317.png)

<center style="color:#C0C0C0;text-decoration:underline">ANN的隐含层</center>

上图展示了深度神经网络中的一层可配置，单隐含层，包括选择信号SelX，突触S，神经元N

![image-20220301153654122](C:\Users\ziv\AppData\Roaming\Typora\typora-user-images\image-20220301153654122.png)

<center style="color:#C0C0C0;text-decoration:underline">突触的电路图</center>

在上图中，通过控制B0~B4，调节尾电流。图的上半部分是一个差分电路，通过B5控制Iout+和Iout-的选择。

![image-20220301154157049](C:\Users\ziv\AppData\Roaming\Typora\typora-user-images\image-20220301154157049.png)

<center style="color:#C0C0C0;text-decoration:underline">神经元的电路图</center>

神经元电路将突触输出，即差分电流，转换为差分电压。

对于训练算法的选择，使用最小均方误差，和模拟退火避免陷入局部最小。

实验结果：使用硬件神经网络和Matlab上的软件神经网络相比，训练误差更大，但是验证误差有可比性。但是如果在隐含层包含更多的神经元，则会导致较大的训练误差和验证误差。

缺点：

- 精度比较差，训练时间很长
- 权重的存储需要细致考虑，因为这些权重需要长时间存储但是由可变
- 基于ml的方法是否考虑了DUT在器件生命周期内的DUT degradation的影响

##### 自适应射频前端设计
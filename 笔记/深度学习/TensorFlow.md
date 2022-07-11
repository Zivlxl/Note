##### TensorFlow常见函数

`tf.cast(张量名,dtype=数据类型)` #强制tensor转换成该数据类型

`tf.reduce_min(张量名)、tf.reduce_max()` #计算张量维度上元素的最小（大）值

理解axis

在一个二维张量或数组中，可以调整axis等于1或0控制执行维度。axis=0代表跨行，axis代表跨列。

`tf.reduce_mean(张量名, axis=操作轴)、tf.reduce_sum(张量名, axis=操作轴)` #计算张量沿着指定维度的平均值（和）

`tf.Variable()` #将变量标记为“可训练”，被标记的变量会在反向传播中记录梯度信息。常用该函数标记待训练参数。

`tf.Variable`



数学运算

对应元素的四则运算：`tf.add(张量1, 张量2), tf.subtract, tf.multiply, tf.divide`

平方、次方和开方：`tf.square(张量), tf.pow(张量, 次方), tf.sqrt(张量)`

矩阵乘：`tf.matmul`



`tf.data.Dataset.from_tensor_slice(输入特征, 标签)` #切片传入张量的第一维度，生成输入特征/标签对，构建数据集

```python
features = tf.constant([12, 23, 10, 17])
labels = tf.constant([0, 1, 1, 0])
dataset = tf.data.Dataset.from_tensor_slice(features, labels)
```



`tf.GradientTape` #with结构记录计算过程，gradient求出张量的梯度

```python
with tf.GradientTape() as tape:
    #计算过程
    w = tf.Variable(tf.constant(3.0))
    loss = tf.pow(w, 2)
grad = tape.gradient(loss, w)
print(grad)
'''
tf.Tensor(6.0, shape=(), dtype=float32)
'''
```



`tf.one_hot(待转换数据, depth=几分类)` #独热编码（one-hot encoding）:在分类问题中，常用独热码做标签；标记类型：1为是，0为非

`tf.nn.softmax(x)`



`w.assign_sub(自减的内容)、w.assign_add()` #赋值操作，更新参数的值并返回，自增自减，w必须是Variable

`tf.argmax(张量名, axis=操作轴)` #返回张量沿指定维度最大值的索引



`tf.where(条件语句, 真返回A, 假返回B)` 

```python
a = tf.constant([1, 2, 3, 1, 1])
b = tf.constant([0, 1, 3, 4, 5])

c = tf.where(tf.greater(a, b), a, b) #若a>b，返回a对应位置的元素，否则返回b对应位置的元素

'''
tf.Tensor([1 2 3 4 5], shape=(5,), dtype=int32)
'''
```



##### Tensorflow keras 搭建神经网络

总体步骤：**import->train, test->Sequential/Class->model.complie->model.fit->model.summary**

`model = tf.keras.models.Sequential([网络结构])`  #描述各层网络

网络结构举例：

拉直层：`tf.keras.layers.Flatten()`

全连接层：`tf.keras.layers.Dense(神经元个数, activation="激活函数", kernel_regularizer=哪种正则化)`

activation(字符串)：relu、softmax、sigmoid、tanh

kernel_regularizer：`tf.keras.regularizers.l1()`、`tf.keras.regularizers.l2()`

卷积层：`tf.keras.layers.Conv2D(filters=卷积核个数, kernel_size=卷积核尺寸, strides=卷积步长, padding=valid或same)`

LSTM层：`tf.keras.layers.LSTM()`



`model.compile(optimizer=优化器, loss=损失函数, metrics=['准确率'])` #指定优化器，损失函数

Optimizer可选：

'sgd'或`tf.keras.optimizers.SGD(lr=学习率, momentum=动量参数)`

'adagrad'或`tf.keras.optimizers.Adagrad(lr=学习率)`

'adadelta'或`tf.keras.optimizers.Adadelta(lr=学习率)`

'adam'或`tf.keras.optimizers.Adam(lr=学习率, beta_1=0.9, beta_2=0.999)`

Loss可选：

'mse'或`tf.keras.losses.MeanSquaredError()`

'sparse_categorical_crossentropy'或`tf.keras.losses.SparseCategoricalCrossentropy(from_logits=False)` #false表示神经网络输出前经过了概率分布，所以这里使用false;from_logits = True 表示是原始数据，系统会帮你做softmax后再进行计算

Metrics可选：

'accuracy'：y_和y都是数值

'categorical_accuracy'：y_和y都是独热码，如`y_=[0, 1, 0], y=[0.222, 0.333, 0.555]`

'sparse_categorical_accuracy'：y_数值，y是独热码



`model.fit(训练集的输入特征, 训练集的标签, batch_size=, epochs=, validation_data=(测试集的输入特征, 测试集的标签), validation_split=从训练集划分多少比例给测试集, vaidation_freq=多少次epoch测试一次)`

`model.fit`会返回一个`History`对象，该对象包含一个字典，其中包含训练阶段发生的一切

```python
history = model.fit(...)

history_dict = history.history
print(history.keys())

'''
dict_keys(['loss', 'accuracy', 'val_loss', 'val_accuracy'])
'''
```



`model.summary()` #打印网络结构和参数统计



##### 数据增强（扩充数据集）

`image_gen_train = tf.keras.preprocessing.image.ImageDataGenerator(rescale=所有数据将乘以该值, retation_range=随机旋转角度数范围, width_shift_range=随机宽度偏移量, height_shift_range=随机高度偏移量, horizontal_flip=是否进行随机水平翻转, zoom_range=随机缩放的范围[1-n, 1+n])`

```python
image_gen_train = ImageDataGenerator(
    rescale=1. / 1.0, #如为图像，分母为255时，可归至0~1
    rotation_range=45, #随机45度旋转
    width_shift_range=.15,#宽度偏移
    height_shift_range=.15, #高度偏移
    horizontal_flip=False, #水平翻转
    zoom_range=0.5 #将图像随机缩放阈值50%
)

image_gen_train.fit(x_train) #x_train 要为四维数据 对于MINIST x_train=x_train.reshap(x_train.shape[0], 28, 28, 1)

model.fit(image_gen_train.flow(x_train, y_train, batch_size=32)) #改成这个fit函数
```



##### 断点续训（存取模型）

###### 读取模型

`load_weights(路径文件名)`

```python
checkpoint_save_path = './checkpoint/mnist.ckpt'
if os.path.exists(checkpoint_save_path + '.index'):
	model.load_weights(checkpoint_save_path)
```

###### 保存模型

`tf.keras.callbacks.ModelCheckpoint(file_path=文件路径名, verbose=0, save_weight_only=False, save_best_only=False, mode='auto', save_freq='epoch', period=1,
    options=None, **kwargs)`

**参数**

- **filepath**：字符串，保存模型的路径。
- **monitor**：需要监视的评估指标名。
- **verbose**：详细信息模式，0或1。
- **save_best_only**：如果save_best_only=True，被监测数据的最佳模型就不会被覆盖。
- **mode**： {auto, min, max} 的其中之一。如果 `save_best_only=True`，那么是否覆盖保存文件的决定就取决于被监测数据的最大或者最小值。 对于 `val_acc`，模式就会是 `max`，而对于 `val_loss`，模式就需要是 `min`，等等。在`auto`模式下，方向由被监测值的名字自动推断。
- **save_weights_only**：如果为True，则仅保存模型的权重（model.save_weights(filepath)），否则保存完整模型（model.save(filepath)）。
- **period**：CheckPoint之间的间隔（epoch数）。
- **save_freq**：默认为‘epoch’

**配合`model.fit`使用，`model.fit(...,callbacks=[cp_callback])`**



##### 参数提取

###### 提取可训练参数

`model.trainable_variables` #返回模型中可训练的参数

###### 设置print输出格式

`np.set_printoptions(threshold=超过多少省略显示)`

```python
np.set_printoptions(threshold=np.inf)

print(model.trainable_variables)
file = open('./weights.txt', 'w')
for v in model.trainable_variables:
    file.write(str(v.name) + '\n')
    file.write(str(v.shape) + '\n')    
    file.write(str(v.numpy()) + '\n')    
```



##### 给图识物

前向传播执行应用`model.predict(输入特征, batch_size=整数)`

**复现模型->加载参数->预测结果**

```python
model = tf.keras.models.Sequential([
    tf.keras.layers.Flatten(),
    tf.keras.layers.Dense(128, activation='relu'),
    tf.keras.layers.Dense(10, activation='softmax')]) #复现模型
    
model.load_weights(model_save_path) #加载参数

result = model.predict(x_predict) #预测结果
np.argmax(result)
```


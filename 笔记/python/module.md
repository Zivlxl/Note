#### sys模块

Python中sys模块：该模块提供对解释器使用或维护的一些变量的访问，以及与解释器强烈交互的函数。

`sys.argv `#命令行参数List，第一个元素是程序本身路径
`sys.modules.keys() `#返回所有已经导入的模块列表
`sys.exc_info() `#获取当前正在处理的异常类,exc_type、exc_value、exc_traceback当前处理的异常详细信息
`sys.exit(n)` #程序，正常退出时exit(0)
`sys.hexversion` #获取Python解释程序的版本值，16进制格式如：0x020403F0
`sys.version` #获取Python解释程序的版本信息
`sys.maxint` #最大的Int值
`sys.maxunicode` #最大的Unicode值
`sys.modules` #返回系统导入的模块字段，key是模块名，value是模块
`sys.path` #返回模块的搜索路径，初始化时使用PYTHONPATH环境变量的值
`sys.platform` #返回操作系统平台名称
`sys.stdout` #标准输出
`sys.stdin` #标准输入
`sys.stderr` #错误输出
`sys.exc_clear()` #用来清除当前线程所出现的当前的或最近的错误信息
`sys.exec_prefix` #返回平台独立的python文件安装的位置
`sys.byteorder` #本地字节规则的指示器，big-endian平台的值是'big',little-endian平台的值是'little'
`sys.copyright` #记录python版权相关的东西
`sys.api_version` #解释器的C的API版本
`sys.version_info` #获取Python解释器的版本信息
`sys.getwindowsversion` #获取Windows的版本
`sys.getdefaultencoding` #返回当前你所用的默认的字符编码格式
`sys.getfilesystemencoding` #返回将Unicode文件名转换成系统文件名的编码的名字
`sys.setdefaultencoding(name)` #用来设置当前默认的字符编码
`sys.builtin_module_names` #Python解释器导入的模块列表
`sys.executable` #Python解释程序路径
`sys.stdin.readline` #从标准输入读一行，`sys.stdout.write("a") `屏幕输出a

python程序中使用import X时，python解释器会在**当前目录、已安装和第三方模块中搜索X**，如果都搜索不到就报错。使用`sys.path.append()`方法可以临时添加搜索路径，方便import其他包和模块。这种方法导入的路径会在python退出后失效。

```python
import sys,os

sys.path.append('..') #将上层目录加入
sys.path.append(os.path.abspath(os.path.dirname(__file__))) #加入当前路径

#sys.path.insert 定义搜索路径的优先顺序，序号从0开始，表示最大优先级，sys.path.insert加入的也是临时搜索路径，程序退出后失效
sys.path.insert(0, "./module")
```



#### os模块

os，语义操作系统，所以该模块就是操作系统相关的功能了，用于处理文件和目录这些我们日常手动需要做的操作，比如新建文件夹、获取文件列表、删除某个文件、获取文件大小、重命名文件、获取文件修改时间等，该模块就包含了大量的操作系统操作函数。

`os.name` #显示当前使用平台

`os.getcwd()` #返回当前进程的工作目录

`os.chdir(path)` #改变当前工作目录到指定目录

`os.makedirs(path, mode=0o777)` #递归创建目录，mode为目录的权限

`os.makedir(path, [,mode])` #创建目录

`os.listdir(path)` #列出目录下的所有文件夹和文件

`os.remove(path)` #删除指定路径的文件，如果指定的路径是一个目录，抛出OSError异常

`os.rename(src, dst)` #明明文件偶目录，能对相应的文件进行重命名

`os.renames(old, new)` #递归重命名目录或文件

`os.linesep` #当前平台用于分隔（或终止）行的字符串。它可以是单个字符，如 POSIX 上是 '\n'，也可以是多个字符，如 Windows 上是 '\r\n'。在写入以文本模式（默认模式）打开的文件时，请不要使用 os.linesep 作为行终止符，请在所有平台上都使用一个 '\n' 代替

`os.pathsep` #操作系统通常用于分隔搜索路径（如 PATH）中不同部分的字符，如 POSIX 上是 ':'，Windows 上是 ';'。在 os.path 中也可用

`os.open() os.close()` #

`os.stat(path)` #获取文件或者目录信息

>>> os.stat('./setup.py')
>>> os.stat_result(st_mode=33204, st_ino=7869836, st_dev=2050, st_nlink=1, st_uid=1000, st_gid=1000, st_size=1677, st_atime=1652103963, st_mtime=1652103890, st_ctime=1652103890)

`os.sep` #显示当前平台下路径分隔符,在 POSIX 上是 '/'，在 Windows 上是 '\\'

`os.path.abspath(path)` #返回文件的绝对路径

`os.path.basename(path)` #返回文件名，纯粹字符串处理逻辑，路径错误也可以

>>> os.path.basename('./setup.py')
>>> 'setup.py'

`os.path.commonprefix(list)` #返回list（多个路径）中，所有path共有的最长的路径

`os.path.dirname(path)` #返回文件路径

`os.path.exists(path)` #如果路径 path 存在，返回 True；如果路径 path 不存在，返回 False

`os.path.lexists(path)` #路径存在则返回True，路径损坏也返回True， 不存在，返回 False

`os.path.expanduser(path)`  #把path中包含的"~"和"~user"转换成用户目录

>>> os.path.expanduser('~/remoteres')
>>> '/home/ziv/remoteres'

`os.environ['KKPATH'] = '/home/xxx/xxx'` #配置环境变量

`os.path.expandvars(path)` #根据环境变量的值替换path中包含的"$name"和"${name}"

`os.path.getatime(path)` #返回最近访问时间（浮点型秒数），从新纪元到访问时的秒数

`os.path.getmtime(path)` #返回最近文件修改时间，从新纪元到访问时的秒数

`os.path.getctime(path)` #返回文件 path 创建时间，从新纪元到访问时的秒数

`os.path.getsize(path)` #返回文件大小，如果文件不存在就返回错误

`os.path.isabs(path)` #判断是否为绝对路径，也就是说在WIndow系统下，如果输入的字符串以" / "开头，os.path.isabs()就会返回True

`os.path.isfile(path)` #判断路径是否为文件，文件不存在，返回False

`os.path.isdir(path)` #判断路径是否为目录，路径不存在，返回False

`os.path.join(path1,[,path2[,…]])`  #把目录和文件名合成一个路径,1.如果各组件名首字母不包含’/’，则函数会自动加上,2.如果有一个组件是一个绝对路径，则在它之前的所有组件均会被舍弃,3.如果最后一个组件为空，则生成的路径以一个’/’分隔符结尾

`os.path.split(path)` #把路径分割成 dirname 和 basename，返回一个元组

>>> os.path.splitext('./setup.py')
>>> ('./setup', '.py')

`os.path.splitext()` #分割路径，返回路径名和文件扩展名的元组

>>> os.path.splitext('./setup.py')
>>> ('./setup', '.py')

`os.path.walk(path, visit, arg)` #遍历path，进入每个目录都调用visit函数，visit函数必须有3个参数(arg, dirname, names)，dirname表示当前目录的目录名，names代表当前目录下的所有文件名，args则为walk的第三个参数，**新版本python好像删除了这个方法，使用os.walk()**

`os.walk(path)` #返回一个list，每个list元素也是list，包括parent（列出了目录路径下面所有存在的目录的名称），dirnames（文件夹名），filenames（列出了目录路径下所有文件的名称）

>>> for parent, dirnames, filenames in os.walk('/home/ziv/PycharmProjects'):
>>> ...     print(parent, dirnames, filenames)
>>> ... 
>>> /home/ziv/PycharmProjects ['pythonProject1'] []
>>> /home/ziv/PycharmProjects/pythonProject1 ['.idea', 'stu'] ['main.py']
>>> /home/ziv/PycharmProjects/pythonProject1/.idea ['inspectionProfiles'] ['modules.xml', 'workspace.xml', '.gitignore', 'pythonProject1.iml', 'misc.xml']
>>> /home/ziv/PycharmProjects/pythonProject1/.idea/inspectionProfiles [] ['profiles_settings.xml', 'Project_Default.xml']
>>> /home/ziv/PycharmProjects/pythonProject1/stu [] ['pdf2word.py', 'copt_stu.py', 'tensorflow_stu.py', 'soduku', 'decorator_stu.py', 'module_stu.py', 'thread_stu.py']

`os.path.samefile()` #判断目录或文件是否相同

`os.path.relpath(path, [, start])` #返回从当前目录或 start 目录（可选）到达 path 之间要经过的相对路径。这仅仅是对路径的计算，不会访问文件系统来确认 path 或 start 的存在性或属性

>>> os.path.relpath('/usr/bin/python3.8')
>>> '../../../../usr/bin/python3.8'



#### pyfiglet

`pyfiglet`可以实现艺术字输出

pyfiglet.FigletFont().getFonts()获取所有字体

##### `pyfiglet.Figlet`

>>> import pyfiglet
>>>
>>> print(pyfiglet.Figlet(font='slant').renderText('hello'))
>>>
>>> __         ____
>>> / /_  ___  / / /___ 
>>> / __ \/ _ \/ / / __ \
>>>  / / / /  __/ / / /_/ /
>>> /_/ /_/\___/_/_/\____/ 


>



##### pyfiglet.figlet_format

>>> from pyfiglet import figlet_format
>>> print(figlet_format('hello', font='slant'))
>>> __         ____
>>> / /_  ___  / / /___ 
>>> / __ \/ _ \/ / / __ \
>>>  / / / /  __/ / / /_/ /
>>> /_/ /_/\___/_/_/\____/ 



#### matplotlib.pyplot

```python
import matplotlib.pyplot as plt
import numpy as np
```

##### 绘图类型

| 函数名称  | 描述                                       |
| --------- | ------------------------------------------ |
| Bar       | 绘制条形图                                 |
| Barh      | 绘制水平条形图                             |
| Boxplot   | 绘制箱型图                                 |
| Hist      | 绘制直方图                                 |
| his2d     | 绘制2D直方图                               |
| Pie       | 绘制饼状图                                 |
| Plot      | 在坐标轴上画线或者标记                     |
| Polar     | 绘制极坐标图                               |
| Scatter   | 绘制x与y的散点图                           |
| Stackplot | 绘制堆叠图                                 |
| Stem      | 用来绘制二维离散数据绘制（又称为“火柴图”） |
| Step      | 绘制阶梯图                                 |
| Quiver    | 绘制一个二维按箭头                         |

###### plot

`plt.plot([x], y, [fmt], *, data=None, **kwargs)`  #**x, y：**点或线的节点，x 为 x 轴数据，y 为 y 轴数据，数据可以列表或数组；**fmt：**可选，定义基本格式（如颜色、标记和线条样式）；***\*kwargs：**可选，用在二维平面图上，设置指定属性，如标签，线的宽度等。

如果我们不指定 x 轴上的点，则 x 会根据 y 的值来设置为 **0, 1, 2, 3..N-1**。

`plt.plot([x], y, [fmt], [x2], y2, [fmt2],..., **kwargs)` #划多条线

```python
plt.plot(x,train_accuracy_result,c='red', label='train')
plt.plot(x,test_accuracy_result, c='green', label='test')
plt.xlabel("Epoch")
plt.ylabel("accuracy")
plt.legend(loc="lower left")
plt.show()
```

![](C:\Users\ziv\Pictures\plt\Figure_4.png)



###### 柱状图bar/barh

`plt.bar(h)(x, height, width=0.8, bottom=None, *, align='center', data=None, **kwargs)` #**x**：浮点型数组，柱形图的 x 轴数据；**height**：浮点型数组，柱形图的高度；**width**：浮点型数组，柱形图的宽度；**bottom**：浮点型数组，底座的 y 坐标，默认 0**（理解为起始y坐标）**；**align**：柱形图与 x 坐标的对齐方式，'center' 以 x 位置为中心，这是默认值。 'edge'：将柱形图的左边缘与 x 位置对齐。要对齐右边缘的条形，可以传递负数的宽度值及 align='edge'；***\*kwargs：**：其他参数。

可以通过设置width参数实现一图多柱。

```python
#准备数据
data =[[30, 25, 50, 20],
[40, 23, 51, 17],
[35, 22, 45, 19]]
X = np.arange(4)
'''fig = plt.figure()
#添加子图区域
ax = fig.add_axes([0,0,1,1])'''
#绘制柱状图
plt.bar(X + 0.00, data[0], color = 'b', width = 0.25, label='you')
plt.bar(X + 0.25, data[1], color = 'g', width = 0.25, label='me')
plt.bar(X + 0.50, data[2], color = 'r', width = 0.25, label='he')
plt.legend(loc='upper right')

plt.show()
```

![](C:\Users\ziv\Pictures\plt\Figure_5.png)

bar() 函数提供了一个可选参数`bottom`，该参数可以指定柱状图开始堆叠的起始值，一般从底部柱状图的最大值开始，依次类推。

```python
countries = ['USA', 'India', 'China', 'Russia', 'Germany'] 
bronzes = np.array([38, 17, 26, 19, 15]) 
silvers = np.array([37, 23, 18, 18, 10]) 
golds = np.array([46, 27, 26, 19, 17]) 
# 此处的 _ 下划线表示将循环取到的值放弃，只得到[0,1,2,3,4]
ind = [x for x, _ in enumerate(countries)] 
#绘制堆叠图
plt.bar(ind, golds, width=0.5, label='golds', color='gold', bottom=silvers+bronzes) 
plt.bar(ind, silvers, width=0.5, label='silvers', color='silver', bottom=bronzes) 
plt.bar(ind, bronzes, width=0.5, label='bronzes', color='#CD853F') 
#设置坐标轴
plt.xticks(ind, countries) 
plt.ylabel("Medals") 
plt.xlabel("Countries") 
plt.legend(loc="upper right") 
plt.title("2019 Olympics Top Scorers")
plt.show()
```

![](C:\Users\ziv\Pictures\plt\Figure_6.png)

###### 饼图pie

`plt.pie(x, explode=None, labels=None, colors=None, autopct=None, pctdistance=0.6, shadow=False, labeldistance=1.1, startangle=0, radius=1, counterclock=True, wedgeprops=None, textprops=None, center=0, 0, frame=False, rotatelabels=False, *, normalize=None, data=None)` 

**参数说明：**

- **x**：浮点型数组，表示每个扇形的面积。
- **explode**：数组，表示各个扇形之间的间隔，默认值为0。
- **labels**：列表，各个扇形的标签，默认值为 None。
- **colors**：数组，表示各个扇形的颜色，默认值为 None。
- **autopct**：设置饼图内各个扇形百分比显示格式，**%d%%** 整数百分比，**%0.1f** 一位小数， **%0.1f%%** 一位小数百分比， **%0.2f%%** 两位小数百分比。
- **labeldistance**：标签标记的绘制位置，相对于半径的比例，默认值为 1.1，如 **<1**则绘制在饼图内侧。
- **pctdistance：**：类似于 labeldistance，指定 autopct 的位置刻度，默认值为 0.6。
- **shadow：**：布尔值 True 或 False，设置饼图的阴影，默认为 False，不设置阴影。
- **radius：**：设置饼图的半径，默认为 1。
- **startangle：**：起始绘制饼图的角度，默认为从 x 轴正方向逆时针画起，如设定 =90 则从 y 轴正方向画起。
- **counterclock**：布尔值，设置指针方向，默认为 True，即逆时针，False 为顺时针。
- **wedgeprops** ：字典类型，默认值 None。参数字典传递给 wedge 对象用来画一个饼图。例如：wedgeprops={'linewidth':5} 设置 wedge 线宽为5。
- **textprops** ：字典类型，默认值为：None。传递给 text 对象的字典参数，用于设置标签（labels）和比例文字的格式。
- **center** ：浮点类型的列表，默认值：(0,0)。用于设置图标中心位置。
- **frame** ：布尔类型，默认值：False。如果是 True，绘制带有表的轴框架。
- **rotatelabels** ：布尔类型，默认为 False。如果为 True，旋转每个 label 到指定的角度。

```python
y = np.array([35, 25, 25, 15])

plt.pie(y,
        labels=['A','B','C','D'], # 设置饼图标签
        colors=["#d5695d", "#5d8ca8", "#65a479", "#a564c9"], # 设置饼图颜色
        explode=[0, 0.2, 0, 0],#第二部分突出显示，值越大，距离越远
        autopct='%.2f%%',#格式化输出百分比
       )
plt.title("Pie Test") # 设置标题
plt.show()
```

![](C:\Users\ziv\Pictures\plt\Figure_7.png)

###### 直方图hist

`plt.hist(x, bins=None, range=None, density=False, weights=None, cumulative=False, bottom=None, histtype='bar', align='mid', orientation='vertical', rwidth=None, log=False, color=None, label=None, stacked=False, *, data=None, **kwargs)`

**参数说明**：

- **x** : (n,) array or sequence of (n,) arrays
  这个参数是指定每个bin(箱子)分布的数据,对应x轴
- **bins** : integer or array_like, optional
  这个参数指定bin(箱子)的个数,也就是总共有几条条状图
- **density** : boolean, optional
  If True, the first element of the return tuple will be the counts normalized to form a probability density, i.e.,n/(len(x)`dbin)
  这个参数指定密度,也就是每个条状图的占比例比,默认为1
- **color** : color or array_like of colors or None, optional
  这个指定条状图的颜色
- **facecolor**: 直方图颜色
- **edgecolor**: 直方图边框颜色
- **alpha**: 透明度
- **histtype**: 直方图类型，‘bar’, ‘barstacked’, ‘step’, ‘stepfilled’

```python
from scipy.stats import norm

# example data
mu = 100  # mean of distribution
sigma = 15  # standard deviation of distribution
x = mu + sigma * np.random.randn(10000)

num_bins = 50
# the histogram of the data
n, bins, patches = plt.hist(x, num_bins, facecolor='blue', alpha=0.5, density=True)
# add a 'best fit' line
y = norm.pdf(bins, mu, sigma)
plt.plot(bins, y, 'r--')
plt.xlabel('Smarts')
plt.ylabel('Probability')
plt.title(r'Histogram of IQ: $\mu=100$, $\sigma=15$')

# Tweak spacing to prevent clipping of ylabel
plt.subplots_adjust(left=0.15)
plt.show()
```

![](C:\Users\ziv\Pictures\plt\Figure_8.png)

###### 散点图scatter

`plt.scatter(x, y, s=None, c=None, marker=None, cmap=None, norm=None, vmin=None, vmax=None, alpha=None, linewidths=None, *, edgecolors=None, plotnonfinite=False, data=None, **kwargs)`

**参数说明：**

- **x，y**：长度相同的数组，也就是我们即将绘制散点图的数据点，输入数据。
- **s**：点的大小，默认 20，也可以是个数组，数组每个参数为对应点的大小。
- **c**：点的颜色，默认蓝色 'b'，也可以是个 RGB 或 RGBA 二维行数组。
- **marker**：点的样式，默认小圆圈 'o'。
- **cmap**：Colormap，默认 None，标量或者是一个 colormap 的名字，只有 c 是一个浮点数数组的时才使用。如果没有申明就是 image.cmap。
- **norm**：Normalize，默认 None，数据亮度在 0-1 之间，只有 c 是一个浮点数的数组的时才使用。
- **vmin，vmax：**：亮度设置，在 norm 参数存在时会忽略。
- **alpha：**：透明度设置，0-1 之间，默认 None，即不透明。
- **linewidths：**：标记点的长度。
- **edgecolors：**：颜色或颜色序列，默认为 'face'，可选值有 'face', 'none', None。
- **plotnonfinite：**：布尔值，设置是否使用非限定的 c ( inf, -inf 或 nan) 绘制点。
- ***\*kwargs：**：其他参数。

```python
# 随机数生成器的种子
np.random.seed(19680801)


N = 50
x = np.random.rand(N)
y = np.random.rand(N)
colors = np.random.rand(N)
area = (30 * np.random.rand(N))**2  # 0 to 15 point radii

plt.scatter(x, y, s=area, c=colors, alpha=0.5) # 设置颜色及透明度

plt.title("Scatter Test") # 设置标题

plt.show()
```

![](C:\Users\ziv\Pictures\plt\Figure_9.png)

颜色条colormap

Matplotlib 模块提供了很多可用的颜色条，颜色条就像一个颜色列表，其中每种颜色都有一个范围从 0 到 100 的值。使用**`plt.colormaps()`**查看所有的颜色条

```python
x = np.array([5,7,8,7,2,17,2,9,4,11,12,9,6])
y = np.array([99,86,87,88,111,86,103,87,94,78,77,85,86])
colors = np.array([0, 10, 20, 30, 40, 45, 50, 55, 60, 70, 80, 90, 100])

plt.scatter(x, y, c=colors, cmap='afmhot_r')
plt.colorbar()
plt.show()
```

![](C:\Users\ziv\Pictures\plt\Figure_10.png)



##### Image函数

| 函数名称 | 描述                               |
| -------- | ---------------------------------- |
| Imread   | 从文件中读取图像的数据并形成数组。 |
| Imsave   | 将数组另存为图像文件。             |
| Imshow   | 在数轴区域内显示图像。             |

##### Axis函数

| 函数名称 | 描述                          |
| -------- | ----------------------------- |
| Axes     | 在画布(Figure)中添加轴        |
| Text     | 向轴添加文本                  |
| Title    | 设置当前轴的标题              |
| Xlabel   | 设置x轴标签                   |
| Xlim     | 获取或者设置x轴区间大小       |
| Xscale   | 设置x轴缩放比例               |
| Xticks   | 获取或设置x轴刻标和相应标签   |
| Ylabel   | 设置y轴的标签                 |
| Ylim     | 获取或设置y轴的区间大小       |
| Yscale   | 设置y轴的缩放比例             |
| Yticks   | 获取或设置y轴的刻标和相应标签 |



##### Figure函数

| 函数名称 | 描述             |
| -------- | ---------------- |
| Figtext  | 在画布上添加文本 |
| Figure   | 创建一个新画布   |
| Show     | 显示数字         |
| Savefig  | 保存当前画布     |
| Close    | 关闭画布窗口     |



##### 其他函数

`plt.pause(iterval)` #暂停间隔多少秒

`plt.cla()` # 清除axes，即当前 figure 中的活动的axes，但其他axes保持不变。

`plt.clf() `# 清除当前 figure 的所有axes，但是不关闭这个 window，所以能继续复用于其他的 plot。

`plt.close()` # 关闭 window，如果没有指定，则指当前 window。



`plt.grid()` #显示网格线

`plt.grid(b, which, axis, color, linestyle, linewidth， **kwargs)`

**参数**

-  b : 布尔值。就是是否显示网格线的意思。官网说如果b设置为None， 且kwargs长度为0，则切换网格状态。
-  which : 取值为'major', 'minor'， 'both'。 默认为'major'。
-  axis : 取值为‘both’， ‘x’，‘y’。就是想绘制哪个方向的网格线。
- color : 这就不用多说了，就是设置网格线的颜色。或者直接用c来代替color也可以。
- linestyle :也可以用ls来代替linestyle， 设置网格线的风格，是连续实线，虚线或者其它不同的线条。 | '-' | '--'             | '-.' | ':' | 'None' | '' | '']
-  linewidth : 设置网格线的宽度



##### 绘制多图

`plt.subplot(nrows, ncols, index)` #nrows和ncols分别表示要划分的行数和列数，index初始值为1，表示选中的区域

```python
import matplotlib.pyplot as plt
plt.plot([1,2,3])
#现在创建一个子图，它表示一个有2行1列的网格的顶部图。
#因为这个子图将与第一个重叠，所以之前创建的图将被删除
plt.subplot(211)
plt.plot(range(12))
#创建带有黄色背景的第二个子图
plt.subplot(212, facecolor='y')
plt.plot(range(12))
```

![Figure_1](C:\Users\ziv\Pictures\plt\Figure_1.png)

`fig.addsubplot()`

```python
fig = plt.figure()
ax1 = fig.add_subplot(111)
ax1.plot([1,2,3])
ax2 = fig.add_subplot(221, facecolor='y')
ax2.plot([1,2,3])
plt.show()
```

![](C:\Users\ziv\Pictures\plt\Figure_2.png)

通过给画布添加 axes 对象可以实现在同一画布中插入另外的图像。

```python
x = np.arange(0, math.pi*2, 0.05)
fig=plt.figure()
axes1 = fig.add_axes([0.1, 0.1, 0.8, 0.8]) # main axes
axes2 = fig.add_axes([0.55, 0.55, 0.3, 0.3]) # inset axes
y = np.sin(x)
axes1.plot(x, y, 'b')
axes2.plot(x,np.cos(x),'r')
axes1.set_title('sine')
axes2.set_title("cosine")
plt.show()
```

![](C:\Users\ziv\Pictures\plt\Figure_3.png)



#### timeit

python中的timeit模块可以用来测试一段代码的执行耗时，如一个变量赋值语句的执行时间，一个函数的运行时间等。timeit模块是Python标准库中的模块，无需安装，直接导入就可以使用，导入时直接使用`import timeit`可以使用`timeit()`函数和`repeat()`函数，还有Timer类。

`timeit(stmt="pass", setup="pass", timer=default_timer, number=default_number)`

**参数说明：**

- **stmt:**传入需要测试时间的代码，可以直接传入代码表达式或单个变量，也可以传入函数。传入函数时要在函数名后面加上小括号，让函数执行，如 stmt = ‘func()' 
- **setup**：传入 stmt 的运行环境，如 stmt 中使用到的参数、变量，要导入的模块等，如 setup = ‘from \_\_main\_\_ import func' (\_\_main\_\_表示当前的文件)。可以写一行语句，也可以写多行语句，写多行语句时用分号隔开。
- **timer**: timer 参数是当前操作系统的基本时间单位，默认会根据当前运行环境的操作系统自动获取(源码中已经定义)，保持默认即可。
- **number**：要测试的代码的运行次数，默认1000000(一百万)次，对于耗时的代码，运行太多次会花很多时间，可以自己修改运行次数。



`repeat(stmt="pass", setup="pass", timer=default_timer, repeat=default_repeat, number=default_number)`

参数和`timeit`相同

**repeat**：表示测试要重复几次，可以理解为将相同参数的 timeit() 函数重复执行。最终的结果构成一个列表返回，repeat 默认为3次。



在 `Timer`类中，实现了两个方法，`timeit()` 方法和` repeat()` 方法，上面两个函数调用的就是这两个方法。

在使用` from timeit import ...` 时，只能导入` Timer` 类，所以可以直接使用 `Timer` 类来测试，可以自己去调用方法，使用起来更灵活。

```python
timer_insert = timeit.Timer(stmt='insert_time_test()', setup='from __main__ import insert_time_test')
insert_time_timeit = timer_insert.timeit(number=1000000)
print('insert_time_timeit: ', insert_time_timeit)
insert_time_repeat = timer_insert.repeat(number=1000000)
print('insert_time_repeat: ', insert_time_repeat)

'''
('insert_time_timeit: ', 2.7732486)
('insert_time_repeat: ', [2.7367806999999997, 2.707402600000001, 2.7288245999999994])
'''
```


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
sys.path.append(os.path.abspath(os.patth.dirname(__file__))) #加入当前路径

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




### 装饰器

装饰器的作用就是为已经存在的函数或对象添加额外的功能。

装饰器本质上是一个python函数，他可以让其他函数在不需要做任何代码变动的前提下增加额外功能，装饰器的返回值也是一个函数对象。它经常用于有切面要求的场景，比如：插入日志、性能测试、实物处理、缓存、权限校验等场景 。装饰器是解决这类问题的绝佳设计，有了装饰器，我们就可以抽离出大量与函数功能本身无关的雷同代码并继续重用。



#### 无参装饰器

```python
def debug(func):
    def wrapper():
        print('[DEBUG]: enter {}()'.format(func.__name__))
        return func()

    return wrapper

@debug
def say_hello():
    print('hello!')

@debug
def say_goodbye():
    print('goodbye!')


say_hello()
say_goodbye()

‘‘‘
[DEBUG]: enter say_hello()
hello!
[DEBUG]: enter say_goodbye()
goodbye!
’’’
```

将@debug放在函数say_hello()前面，相当于执行了say_hello=debug(say_hello)。debug是一个装饰器，返回了wrapper函数，所以原来的say_hello()依然存在，只是现在同名的now变量指向了新的函数，于是调用say_hello()将执行新的函数，即在debug()函数中返回的wrapper()函数。



可变参数装饰器

```python
def timeit(f):
    def wrapper(*args, **kwargs):
        start_time = time.time()
        res = f(*args, **kwargs)
        end_time = time.time()
        print("%s函数运行时间:%.2f" % (f.__name__, end_time - start_time))
        return res

    return wrapper
```

Python提供了可变参数*args和关键字参数**kwargs，有了这两个参数，装饰器就可以用于任意目标函数。



#### 高阶装饰器


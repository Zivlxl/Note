### JSON

在不同的编程语言传递对象，需要吧对象序列化为标准格式，例如XML，但是更好的方法是使用JSON，因为JSON表示出来就是一个字符串，能被所有语言读取，也方便存储到磁盘或者网络传输。JSON不仅是标准格式，而且比XML更快，可以直接在Web中读取。

JSON格式如下：

```python
p = '{"name": "Bob", "languages": ["Python", "Java"]}'
```



#### JSON和python中数据类型对照

| Python                | JSON Equivalent |
| :-------------------- | :-------------- |
| `dict`                | object          |
| `list`, `tuple`       | array           |
| `str`                 | string          |
| `int`, `float`, `int` | number          |
| `True`                | true            |
| `False`               | false           |
| `None`                | null            |



#### 解析JSON

##### JSON到dict

使用`json.loads()`把JSON转换成dict

```python
import json

person = '{"name": "Bob", "languages": ["English", "French"]}'
person_dict = json.loads(person)

# Output: {'name': 'Bob', 'languages': ['English', 'French']}
print( person_dict)

# Output: ['English', 'French']
print(person_dict['languages'])
```



##### dict到JSON

使用`json.dumps()`把dict转换成JSON

```python
import json

person_dict = {'name': 'Bob',
'age': 12,
'children': None
}
person_json = json.dumps(person_dict)

# Output: {"name": "Bob", "age": 12, "children": null}
print(person_json)
```



##### class到JSON

同样使用`json.dumps()`，但是利用default参数提供将class转换成dict的方法

```python
import json

class Student(object):
    def __init__(self, name, age, score):
        self.name = name
        self.age = age
        self.score = score

person = Student('Bob', 20, 88)

def student2dict(std):
    return {
        'name': std.name,
        'age': std.age,
        'score': std.score
    }

#使用lamda函数
json.dumps(person, default = lambda obj: obj.__dict__)
#自定义转换函数
json.dumps(s, default=student2dict)
```



#### 文件交互

##### 从文件读取

使用`json.load()`从文件中读取JSON

```python
import json

with open('path_to_file/person.json', 'r') as f:
  data = json.load(f)

# Output: {'name': 'Bob', 'languages': ['English', 'French']}
print(data)

#如果JSON文件中有多个条目,data返回是一个list
# Output: [{'name': 'Bob', 'languages': ['English', 'French']}, {'name': 'joe', 'languages': ['English', 'Grecee']}]
print(data)
```



##### 写入文件

使用`json.dump()`写JSON到指定文件

```python
import json

person_dict = {"name": "Bob",
"languages": ["English", "French"],
"married": True,
"age": 32
}

with open('person.txt', 'w') as json_file:
  json.dump(person_dict, json_file)

#Output
#{"name": "Bob", "languages": ["English", "French"], "married": true, "age": 32}
```



#### 美化JSON输出

通过在`json.dumps()`和`json.dump()`方法中设置`indent`、`sort_keys`参数改变输出格式。

```python
import json

person_string = '{"name": "Bob", "languages": "English", "numbers": [2, 1.6, null]}'

# Getting dictionary
person_dict = json.loads(person_string)

# Pretty Printing JSON string back
print(json.dumps(person_dict, indent = 4, sort_keys=True))

#Output
‘‘‘
{
    "languages": "English",
    "name": "Bob",
    "numbers": [
        2,
        1.6,
        null
    ]
}

'''
```


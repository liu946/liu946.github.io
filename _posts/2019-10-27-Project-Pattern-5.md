---
layout: plain
title: 项目模式（五）—— 数据处理流程
category: tech
---


这个话题相比之前的话题非常老套且现实。其涉及如下多个方面的问题。

数据处理在项目中应该是一个什么地位？一般来说，对于一个项目，常见的做法是放一个 `script` 文件夹去管理所有的数据，每次数据从文件输入，并从文件输出。最终处理成想要的格式。顶多再放一个 `run.sh` 去将所有的管理起来。以一个顺序去运行。这种方案在大多数的系统中是没有任何问题的。也推荐这种写法。不过我们再此处讨论的是对于更复杂的系统应该怎样处理。有必要时，你可能将其作为一个独立的项目进行管理。

### 数据的定义

1. 一般来说，使用语言中提供的基本数据类型，或者将其组合即可。
2. 下面我给出一种层叠的对象结构的存储模式。

通过集成基础类型实现如下功能：

1. 方便通过不同的常用协议写入写出（json object, json_list, ndjson）这里有个问题。我们一般定义数据单元的类型，如“句子”但是我们要存储的往往是他们的数组，这应该如何处理？
2. 使用时不应过于复杂。
3. 数据可以先构造，随时对其中的值进行存取。
4. 既然要实现数据结构，那么也最好能在其上定义一些方法。
5. 和之前说的思想一致，不要使用幻数（字符串），引发typo。
6. 给每个字段以初值，以便先构造，再赋值。

实现之后可以类似这样：

```python
from data_base import DataItem, OtherItemField, OtherItemListField

# defination

class Author(DataItem):
    def __init__(self, id=0, name='', level=''):
        self.id = id
        self.name = name
        self.level = level

class Comment(DataItem):
    _fields = {'author': OtherItemField(Author) }
    def __init__(self, id=0, content=None, author=None):
        self.id = id
        self.content = content or []
        self.author = author

class Passage(DataItem):
    _fields = {
        'conment': OtherItemListField(Comment),
        'author': OtherItemField(Author),
    }
    def __init__(self, id=0, content=None, comments=None, author=None):
        self.id = id
        self.content = content or []
        self.comments = comments or []
        self.author = author

## 以上定义描述了一个passage由一个id，一个数组的content，一个数组的Comment和一个author组成。
## 所有的类都知道自己的依存关系，他们通过DataItem实现了如何将自己转化为基础类型并保存和加载。
## 除此之外，使用起来和普通的结构体（数据类）完全一致。

# usage
passages: List[Passage] = Passage.from_ndjson('passage_data_file.jsonl')
for p in passage:
for c in p.comment:
    c.author.level += 1

passage.save_ndjson('new_passage_data_file.jsonl')

## 我们没有做更多的事情，甚至不需要考虑依赖，父类自动帮我们存储了“对象”。
## 令人舒服的是，属性的名字都是标识符，而非字符串（所有的编码都是在提示之下的）。

```

### 数据传递

数据如何在pipeline中传递，通过什么索引，中间数据，处理后的数据应该怎样存放，

- 方案一：

善用 Dict[str, Any] 结构，在处理中，很多中间结果应该被封存在一个字典中。很多系统采用这种模式进行传递，比如Allennlp的模型结构。不过该方案也有缺点，就是键名字问题，容易出错，尽量使其有默认值，并可与在定义的操作类构造时可以指定。

- 方案二：

继承链结构（如果想复用，也可以使用修饰器模式），这种方案甚至不需要配置文件之类，直接树型对处理流进行构造，运行，保存最终结果即可。所有的类的数据可以保存在self的统一接口上，也可以定义通用接口进行懒加载。

### 流程的定义

方案一：

1. 定义为单输入，单输出的pipeline，pipeline通过操作数组描述，数组中的每个操作顺序执行，对之前模块的输出进行处理。

### 流程通用功能

1. 进度条，处理可能需要很久时间，定义好模块名，进度条，方便查看进度。


### 技巧 —— 长时处理cache

数据处理中有一些耗时很长的操作，比如需要分词、句法分析，或者需要动态访问网络资源的。但是我们在处理中往往需要调整规则、流程，这就需要从头运行，运行多次，这样每次运行时间都很长。因此，我们对此进行cache，同时防止运行错误导致的前功尽弃。

下面是我设计的一个对函数调用的自动cache装饰器，加在函数外部即可对内置类型输入输出的函数进行自动cache。

```python
def make_persist(persist_dir='.', persist_file=None):
    def decorator(pure_func):
        file = path.join(persist_dir, persist_file or pure_func)
        arg_value_dict = {}
        if path.isfile(file):
            with open(file, 'r') as f:
                for line in f.readlines():
                    if line.strip():
                        json_obj = json.loads(line)
                        arg_value_dict[tuple(json_obj['key'])] = json_obj['value']

        f = open(file, 'a')

        def wrapper(*args):
            key = tuple(args)
            if key in arg_value_dict:
                return arg_value_dict[key]
            else:
                arg_value_dict[key] = pure_func(*args)
                f.write(json.dumps({'key': key, 'value': arg_value_dict[key]}) + '\n')
                return arg_value_dict[key]
        return wrapper

    return decorator


@make_persist(persist_file='data/persist.double.json')
def double(i: int):
    return i * 2 or None


if __name__ == '__main__':
    for i in range(3):
        for j in range(3):
            print(double(j))

```


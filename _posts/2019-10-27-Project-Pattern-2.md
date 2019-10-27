---
layout: plain
title: 项目模式（二）—— 统一分层配置的动态加载
category: tech
---


### 需求

1. 项目配置的复杂性，需要 1. 对其进行分层定义 2. 不同配置之间可能有依赖
2. 切换配置系统必须是和项目无关的，切换配置对业务模块透明
3. 在编码时可以给出提示（使用IDE可感知的类实现，而不是配置文件、json等），避免typo
4. 实现方便、可读
5. 【Optional】延迟计算：配置被依赖项，子项跟随改变

### 需求分析

目前有一些配置模式可以实现1，比如jsonnet。而且对于所有可以抽象配置文件的系统，也都可以实现2，（2是采用配置的基本能力）。

但是，对于3，一般的配置系统都无法提供（本文中提出的动态加载方案便有所实现，相对的，我放弃了平台兼容性，只是给出了python的方案，其他语言可能有所变化，而向编译式语言可能还不能使用）。在有些系统中（dlab、OpenNMT-py）给出了生成配置文件的方法，将默认的配置文件生成好，再使用配置文件运行，这种模式解决了一半问题（可以解决外部用户的typo问题）

5是建立在实现1中的依赖之上的，如果实现5，这个依赖就是动态依赖。当父类改变时子类跟着改变。在ruby中，我们可以较为方便的按照我们的想法去修改一个类，在python中，我用了tricky的方案，而在其他语言中，可能很难在保证4的前提下实现。

### 防止过设计

1. 注意配置文件的范围，这在不同的项目中可能定义不同。就我的经验而言，一般配置项应该具备如下特点：

    1. 有限且名称固定，尽量不要出现如 ‘gpu-%d-memory-limit’，或者列表
    2. 定义简单一些，尽量避免配置项迭代、递归（allennlp实现了一套优秀的动态配置，对于一般项目并不推荐）
    3. 配置是全局的
    4. 配置是不可变的（对于一次运行）



### 实现

```
.
├── configs
│   ├── base_config.py
│   ├── config1.py
│   └── config2.py
├── project_name
    ├── config.py
    ├── module1
    ├── module2

```

所有模块的配置写到 config/base_config 里，project_name/config.py 中动态引用 configs/base_config.py 或者其他同文件夹下的文件。所有再module里的文件配置去读 project_name/config.py，从中引用配置。

- 动态方式
    
    可以读取机器相关属性（通过操作系统判断环境），读取某个环境名文件(.env模式)，或者其他方式去判断读取哪个配置。

- 配置的重载与覆盖
    
    如果希望实现通过重载父类的方式来修改子类，在python中就需要较为复杂的操作，目的是 1. 需要延迟求值。 2. 需要对名称进行统一管理（因为解释期绑定，即使上下文中对象已经覆盖掉了，解释时也会使用原来的类）。需要使用基类去实现一些trick。下面有一个简单的实现和例子：
    
```python
# in tools.config
class Config(object):

    @classmethod
    def override(cls, by_cls):
        parent__init__ = cls.__init__

        def new__init__(self):
            parent__init__(self)
            by_cls.__init__(self)

        cls.__init__ = new__init__
        return by_cls

# in configs.base
class BaseConfig(Config):
    def __init__(self):
        self.ip = '192.168.1.1'
        self.protocol = 'http'
        self.other = 'other'


class InstanceConfig(BaseConfig):
    def __init__(self):
        super().__init__()
        self.address = f'{self.ip}:5000'


# in configs.local 动态加载，覆盖
@BaseConfig.override
class NewBaseConfig(BaseConfig):
    # noinspection PyMissingConstructor
    def __init__(self):
        self.ip = '127.0.0.1'
        self.protocol = 'tcp'


# in configs.other 动态加载，覆盖。这里展示的是被覆盖的还可以再依赖，再次覆盖。
#                  但是在此实现中，无法摘除原来的覆盖。所以平行的覆盖要放在不同的文件中（本来配置就是这样的逻辑）
@BaseConfig.override
class NewBaseConfig2(NewBaseConfig):
    # noinspection PyMissingConstructor
    def __init__(self):
        self.protocol = 'scp'


cfg = InstanceConfig()
print(cfg.address)
print(cfg.protocol)
print(cfg.other)
```


### 分析

对于一个比较复杂的项目（一个运行时程序），



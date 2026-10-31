---
title: "Python 学习笔记"
date: "2026-10-31T17:30:00+08:00"
tags: ["Python", "编程", "学习笔记"]
title-images: ["/python/run_01.png"]
ending-images: []
author: "站长"
draft: false
table-of-contents: true
toc-auto-numbering: true
---
<!-- 摘要 -->
这篇文章记录我系统学习 Python 的完整过程：从变量、字符串、数字，到列表、字典、流程控制、函数、面向对象，再到文件读写与异常处理，最后用一个支持本地持久化的命令行待办清单把所有知识点串起来
<!--more-->
<!-- 正文 -->
## 学习环境与准备

开始动手前，我先把开发环境搭好，这样后面写代码、调试、运行都在一个统一的地方完成：

- **实践平台**：PyCharm，用来编写和运行代码；
- **Python 版本**：Python 3.14；
- **虚拟环境**：在项目目录下用 Virtualenv 创建独立的 `.venv`，避免和系统里其他项目的依赖互相干扰；
- **练习方式**：把知识点拆成 8 个脚本，每个脚本聚焦一个主题，写完立刻运行验证。

在 PyCharm 中打开脚本后，按 `Shift + F10` 即可运行，底部的运行窗口会显示完整的命令行、打印输出以及退出代码。下面按主题逐个记录。

## 一、变量、字符串与数字

第一个脚本练习最基础的内容。Python 是**动态类型**语言，变量不需要事先声明类型，直接赋值即可使用。

字符串方面，我练习了常用方法：`strip()` 去除首尾空白、`upper()` 转大写、`title()` 首字母大写，以及用 **f-string** 把变量直接嵌入字符串。数字方面练习了加、除、整除 `//`、取余 `%`、乘方 `**`，并通过 `int()` 和 `str()` 做类型转换。

```python
message = "你好，Python！"
print(message)

name = "  layover  "
print("去除首尾空格：", name.strip())
print("转大写：", name.strip().upper())

age = 20
intro = f"我今年 {age} 岁，学习 Python 第 1 天"
print(intro)

a, b = 17, 5
print("整除", a // b, "取余", a % b, "乘方", b ** 2)

price = int("99") + 1
print("数字转字符串：", str(price) + " 元")
```

一个需要记住的细节：单斜杠 `/` 的除法结果**永远是浮点数**，即使能整除也会返回带小数点的结果；想要整数结果要用 `//`。

![变量、字符串与数字的运行结果](/python/run_01.png)

## 二、列表与元组

列表是 Python 里最常用的**有序可变集合**，用方括号表示。我练习了通过下标访问元素（`-1` 表示最后一个）、`append()` 末尾添加、`insert()` 指定位置插入、按下标修改、`remove()` 按值删除，以及用 `for` 循环遍历。

```python
fruits = ["苹果", "香蕉", "橙子", "葡萄"]
fruits.append("西瓜")
fruits.insert(0, "草莓")
fruits[1] = "红苹果"
fruits.remove("橙子")

for fruit in fruits:
    print("  -", fruit)
```

此外还有两个非常实用的特性：

- **列表推导式**：用一行代码生成新列表，例如 `[n ** 2 for n in numbers]` 快速算出平方列表；
- **切片**：`fruits[:3]` 取前 3 个，`fruits[1:4]` 取指定区间，切片遵循“左闭右开”，且不会越界报错。

元组则用圆括号表示，和列表最大的区别是**元素不可修改**，适合存放固定不变的数据，比如屏幕分辨率 `(1920, 1080)`。

![列表与元组的运行结果](/python/run_02.png)

## 三、字典：键值对存储

字典用来存放**键值对**，用花括号表示，通过键而不是下标来取值。我练习了用 `[键]` 和 `get()` 访问、新增和修改键值对，以及用 `items()` 同时遍历键和值。

```python
student = {"姓名": "小明", "年龄": 18, "专业": "计算机科学", "是否在读": True}
student["年级"] = "大二"
student["年龄"] = 19

for key, value in student.items():
    print(f"  {key} -> {value}")
```

字典还可以**嵌套**成“字典列表”，用来表示一组结构相同的记录。下面用一个班级名单练习嵌套遍历，并结合生成器表达式计算平均成绩：

```python
students = [
    {"姓名": "小明", "成绩": 88},
    {"姓名": "小红", "成绩": 95},
    {"姓名": "小刚", "成绩": 76},
]
avg = sum(s["成绩"] for s in students) / len(students)
print(f"班级平均成绩：{avg:.1f} 分")
```

运行后平均成绩为 86.3 分。其中 `:.1f` 表示把浮点数保留一位小数。

![字典的运行结果](/python/run_03.png)

## 四、条件判断与循环

这一部分练习让程序“做判断”和“重复执行”。条件判断用 `if / elif / else`，配合比较运算符把分数转换成等级；多个条件可以用 `and`、`or`、`not` 等逻辑运算符组合。

```python
score = 82
if score >= 90:
    grade = "优秀"
elif score >= 80:
    grade = "良好"
elif score >= 60:
    grade = "及格"
else:
    grade = "不及格"
```

循环有两种：`for` 循环适合已知次数的遍历，常搭配 `range()` 生成数字序列；`while` 循环会在条件成立时不断执行，适合不确定次数的场景。我用 `while` 模拟了一个逐步逼近目标数字的猜数字过程。

```python
total = 0
for i in range(1, 6):
    total += i
print("1 到 5 的累加结果：", total)
```

循环里还有两个控制关键字：`break` 用来**立即跳出**整个循环，`continue` 用来**跳过当前这一轮**直接进入下一次。下面用 `continue` 只打印偶数、跳过奇数：

```python
for n in range(10):
    if n % 2 != 0:
        continue
    print("  偶数：", n)
```

![流程控制的运行结果](/python/run_04.png)

## 五、函数

函数是**可复用的代码块**，用 `def` 定义，通过 `return` 把结果返回给调用处。我练习了带返回值的普通函数、默认参数、关键字参数，以及两种可变参数。

```python
def greet(name):
    return f"你好，{name}！欢迎学习 Python。"
```

默认参数在调用时可以省略，关键字参数则通过“参数名=值”的方式传递，顺序可以自由安排：

```python
def describe_pet(pet_name, animal="狗"):
    return f"我有一只{animal}，名字叫{pet_name}。"

print(describe_pet("旺财"))
print(describe_pet(animal="猫", pet_name="咪咪"))
```

当参数个数不确定时：

- `*args` 收集任意数量的**位置参数**，打包成元组，比如 `make_pizza(9, "芝士", "蘑菇", "培根")`；
- `**kwargs` 收集任意数量的**关键字参数**，打包成字典，用来组装用户资料。

最后我还写了一个 BMI 计算函数，用 `round()` 把结果保留一位小数，运行结果为 19.6。

![函数的运行结果](/python/run_05.png)

## 六、面向对象：类与继承

面向对象把数据和操作数据的方法封装成**类**，再由类创建具体的**实例（对象）**。`__init__` 是初始化方法，创建实例时自动调用，`self` 代表当前对象本身。

```python
class Dog:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def sit(self):
        print(f"{self.name} 坐下了！")

    def bark(self):
        print(f"{self.name} 汪汪叫！")

my_dog = Dog("旺财", 3)
my_dog.sit()
```

**继承**让子类复用父类的属性和方法。子类的 `__init__` 里通过 `super().__init__()` 调用父类的初始化方法，既拥有父类的能力，又能扩展自己的新方法：

```python
class GuideDog(Dog):
    def __init__(self, name, age, owner):
        super().__init__(name, age)
        self.owner = owner

    def guide(self):
        print(f"{self.name} 正在为 {self.owner} 引路。")
```

我还写了一个 `Car` 类练习通过方法修改属性：`drive()` 被调用后里程数会累加，体现了对象可以保存并维护自己的状态。

![类与继承的运行结果](/python/run_06.png)

## 七、文件读写与异常处理

这一部分练习把数据保存到磁盘，以及让程序在出错时不崩溃。读写文件推荐用 `with` 语句，它会在代码块结束后**自动关闭文件**，即使中途出错也能正确释放资源。

```python
with open("notes.txt", "w", encoding="utf-8") as f:
    f.write("第一行：学习 Python 基础语法\n")
    f.write("第二行：理解列表和字典\n")
```

打开模式中，`w` 表示写入（会覆盖原内容）、`a` 表示追加、`r` 表示读取。读取时可以直接用 `for` 逐行遍历，也可以用 `readlines()` 把所有行读成一个列表。加上 `encoding="utf-8"` 可以保证中文不乱码。

异常处理用 `try / except / finally`：把可能出错的代码放进 `try`，捕获到对应错误后在 `except` 中处理，`finally` 里的代码无论是否出错都会执行。

```python
try:
    result = 10 / 0
except ZeroDivisionError:
    print("  捕获到错误：除数不能为 0")
finally:
    print("  无论是否出错，这行都会执行")
```

我分别练习了捕获除零错误 `ZeroDivisionError` 和文件不存在错误 `FileNotFoundError`，程序都平稳运行而没有崩溃。

![文件与异常的运行结果](/python/run_07.png)

## 八、命令行待办清单

最后一个脚本是综合项目，把前面学到的**类、函数、列表、字典、循环、文件读写、异常处理**全部用上，做一个支持本地持久化的命令行待办清单。

核心设计是一个 `TodoList` 类：任务用“字典列表”保存，每条任务包含编号、标题和完成状态；每次增删改后都调用 `_save()` 写进 `todos.json`，启动时用 `_load()` 读取，文件不存在或格式错误时安全地返回空列表。

```python
class TodoList:
    def __init__(self, storage_file="todos.json"):
        self.storage_file = storage_file
        self.tasks = self._load()

    def add(self, title):
        task = {"id": len(self.tasks) + 1, "title": title, "done": False}
        self.tasks.append(task)
        self._save()

    def complete(self, task_id):
        for task in self.tasks:
            if task["id"] == task_id:
                task["done"] = True
                self._save()
                return

    def show(self):
        for task in self.tasks:
            status = "✓" if task["done"] else "○"
            print(f"  [{status}] {task['id']}. {task['title']}")
```

这里借助标准库 `json` 实现数据持久化，`json.dump()` 写入时加上 `ensure_ascii=False` 可以让中文直接保存而不是转义成编码。运行后可以看到：先添加 3 条任务（进度 0/3），完成前 2 条后再次展示（进度 2/3），并且任务已经写入本地文件，下次启动会自动加载。

![综合项目待办清单的运行结果](/python/run_08.png)



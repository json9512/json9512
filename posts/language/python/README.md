# Python
- 파이썬은 원래 가독성이 좋은 프로그래밍 언어
- 가독성을 살려서 코드를 작성하게끔 pythonic 한 가이드라인이 있음
- Python coding convention과 흔히 접하지 않는 것들에 대해 알아보자

Reference: [Python Code Styles](https://docs.python-guide.org/writing/style/)

# Content
1. [General Rules](#general-rules)
2. [Idioms](#idioms)
3. [Advanced Topics](#advanced-topics)

****

# General Rules
## 1. Explicit code

**Bad**
```python
def make_complex(*args):
    x, y = args
    return dict(**locals())
```

**Good**
```python
def make_complex(x, y):
    return {'x': x, 'y': y}
```

딱 보면 무슨 코드인지 알 수 있도록 (self-explanatory)

## 2. One statement per line

**Bad**
```python
print 'a'; print 'b'

if x == 1: print 'a'

if <complex comparison> and <complex comparison>:
    # do some'in
```

**Good**
```python
print 'a'
print 'b'

if x == 1: 
    print 'a'

condition1 = <complex comparison>
condition2 = <complex comparison>

if condition1 and condition2:
    # do some'in
```

## 3. Function arguments
4 가지 방법이 있음
1. positional arguments - `send(message, recipient) -> send("Hello", "God")`, `point(x, y) -> point(0, 35)` <br>function 구동에 무조건 필요한 arguments
2. keyword arguments - `send(message, to, cc=None) -> send("Hello", "God", "Mom") or send("Hello", "God")`<br>기본값을 지정한 argument; function 구동에 필수적이지 않은 argument (`cc`)  
3. arbitrary argument list - `send(message, *args) -> send("Hello", "God", "Mom", "Dad"` <br>`message` argument 이후에 하나의 tuple로 입력 arguments를 저장함; tuple에 저장되는 값의 type이 다 다를 때 사용하는 것이 유용함
4. arbitrary keyword argument dictionary - `send(message, **kwargs) -> send("Hello", to=God, cc=Mom)`

개발자의 판단에 따라 가장 적합한 방식으로 코드를 짜면 됨

## 4. Don't use the magical wand
파이썬은 customizable하다. 하지만 기본적으로 작동되는 방식을 바꾸게 되면 가독성이 떨어진다.

정말 필요할 때가 아니면 하지 말자

## 5. We are all responsible users
파이썬은 다른 언어에 있는 `private` 변수나 클래스 같은 것들이 기본적으로 사용되지 않는다. 이는 Java와 같이 방어적(?)인 언어들과 다르다. 

이유는 python 개발자는 모두 책임감이 있다고 믿기 때문이다. 개발자로서 자신이 사용하면 안되는 코드/특성은 사용을 하지 않는 것이 좋다.

하지만 `private` 특성을 만들지 못하거나 encapsulation이 불가능 하다는 뜻이 아니다. 

`__`를 특성/함수 앞에다가 붙이면 된다.

```python
class Foo:
    '''
        __test = "Ac"
    '''
    def __init__(self):
        self.__test = "Ac"

    def __print_me(self):
        print(self.__test)

# outside
b = Foo()
b.__print_me() # no attribute error
print(b.__test) # no attribute error
```
## 6. Returning Values
- 함수가 복잡할수록 여러 곳에서 return 을 할 때가 종종 있다. 하지만 가독성을 중요시하고 코드가 더 직관적이고자 한다면, 여러 곳에서 return을 하는 것은 좋지 않다 

- 보통 2가지의 경우에 함수에서 return을 한다
    1. 로직을 따라 정상처리가 됐을 때 
    2. 에러가 났을 때

- Refactoring을 위해 하나의 return 포인트를 유지 하는 것이 좋다

```python
def complex_function(a, b):
    if not a:
        return None # raising an exception might be better
    
    if not b: 
        return None # raising an exception might be better
    
    # Some complex code to compute x from a, b
    # Resist temptation to return when compute succeeds

    if not x:
        # some code to compute x as plan-b
    return x # single exit point for maintainability

```

# Idioms
- pythonic 한 코드를 작성하는 방법은 아래와 같다

## 1. Unpacking values

1. 리스트에서 아이템 추출 시 `enumerate()` 함수 사용
```python
for index, item in enumerate(some_list):
    # do some'in with index and item
```

2. 변수끼리 swap 할 때 
```python
# common 
temp = b
b = a
a = temp

# pythonic
a, b = b, a
```

3. Nested unpacking
```python
a, (b, c) = 1, (2, 3)

# python 3 (new feature)
a, *rest = [1, 2, 3, 4]
# a = 1, rest = [2, 3, 4]

a, *mid, c = [1, 2, 3, 4]
# a = 1, mid = [2, 3], c = 4
```

## 2. Creating an ignored variable
```python
filename = "awesomefile.txt"
basename, __, ext = filename.rpartition(".")

# basename = awesomefile, __ = ., ext = txt
# use __ to ignore vals
# using _ might conflict since it's an alias for 
# gettext(), and _ is used to store the last operation 
# at the interactive prompt
```

## 3. Creating lists
**A list of length - N**
```python
arr_four = [0] * 4
```

**A list of length - N of lists**
```python
arr_four_nested = [[] for __ in range(4)]
```

**Create a string from list**
```python
some_list = ["a", "b", "c"]
stringified = ''.join(some_list)
```

## 4. Searching items in iterables
```python
some_set = set(["i", "t", "e", "m"])
some_list = ["i", "t", "e", "m"]

cond1 = "t" in some_set
cond2 = "i" in some_set

# Set/Dict is a hash table
# Much faster than lists/tuples when searching a large dataset
# Sometimes using lists is better because creating the hash table requires more memory 
```

## 5. Zen of Python
```python
>>> import this
'''
The Zen of Python, by Tim Peters

Beautiful is better than ugly.
Explicit is better than implicit.
Simple is better than complex.
Complex is better than complicated.
Flat is better than nested.
Sparse is better than dense.
Readability counts.
Special cases aren't special enough to break the rules.
Although practicality beats purity.
Errors should never pass silently.
Unless explicitly silenced.
In the face of ambiguity, refuse the temptation to guess.
There should be one-- and preferably only one --obvious way to do it.
Although that way may not be obvious at first unless you're Dutch.
Now is better than never.
Although never is often better than *right* now.
If the implementation is hard to explain, it's a bad idea.
If the implementation is easy to explain, it may be a good idea.
Namespaces are one honking great idea -- let's do more of those!
'''
```
[With example on github](https://github.com/hblanks/zen-of-python-by-example/blob/master/pep20_by_example.pdf)

## 6. PEP 8 
- defacto code style for python. Available [here](https://pep8.org/)

## 7. Some Conventions
**1. Check if variable equals constant**
```python
# Bad
if attr == True:
    return "True!"

if attr == None:
    return "None!"

# Good
if attr:
    return "True"

if not attr:
    return "False"

if attr is None:
    return "None"
```

**2. Access a dictionary element**
```python
# Bad
d = {"hello": "there"}

# Don't use dict.has_key()
if d.has_key("hello"):
    print(d["hello"])
else:
    print("default_value")

# Good
d = {"hello": "there"}

print(d.get('hello', 'default_value')) # prints 'there'
print(d.get('somein', 'default_value')) # prints 'default_value'

# Or:
if 'hello' in d:
    print(d['hello'])
```

**3. Short ways to manipulate lists**
```python
# Bad - needlessly allocates a list of all (gpa, name) entries in memory
valedictorian = max([(student.gpa, student.name) for student in graduates])

# Good
valedictorian = max((student.gpa, student.name) for student in graduates)
```

```python
# Good
# Generator functions for more complex tasks
def make_batches(items, batch_size):
    '''
    >>> list(make_batches([1, 2, 3, 4, 5], batch_size=3))
    [[1, 2, 3], [4, 5]]

    >>> generator = make_batches([1, 2, 3, 4, 5], batch_size=3)
    >>> next(generator)
    [1, 2, 3]
    '''

    current_batch = []
    for item in items:
        current_batch.append(item)

        if len(current_batch) == batch_size:
            yield current_batch
            current_batch = []

    yield current_batch 
```
```python
# Bad - never use list comprehension for its side effects
[print(x) for x in some_list]

# Good
for x in some_list:
    print(x)
```

**4. Filtering a List**
```python
# Bad - Don't delete items when iterating through the list
a = [3, 4, 5]

for i in a:
    if i > 4:
        a.remove(i)

# Don't make multiple passes through the list
while i in a:
    a.remove(i)

# Good
# comprehensions create a new list object
filtered_values = [value for value in some_list if value > 4]

# generators don't create another list 
filtered_values = (value for value in some_list if value > 4)
```

**5. Modifying the values in a list**
```python
# Bad
a = [3, 4, 5]
b = a # a,b refer to same list object

for i in range(len(a)):
    a[i] += 3 # changing a will also change b

# Good - create a new list object
a = [3, 4, 5]
b = a

a = [i+3 for i in a] # does not change b
```

**6. Read from a file**
```python
# Bad
f = open("file.txt")
a = f.read()
print(a)
f.close()

# Good - with open automatically closes the file
with open("file.txt") as f:
    for line in f:
        print(line)
```

**7. Line Continuations**
```python
# Bad - using "\" might break if there is space afterwards"\ "
some_string = "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa \
    aaaaaaaaaaaaaaaaaaaa"

# Good - open (, [, { will indicate the python interpreter to read until ), ], } closes
some_string = (
    "aaaaaaaaaaaaaaaaaaaaaaaaaaa"
    "aaaaaaaaaaaaaaaaaaaaaaaaaaaa"
    "aaaaaaaaaaaaaaaaaaaaaaaaaaa"
)
```
****
# Advanced Topics

파이썬 개발자라면 알아야 할 [Python design and history](https://docs.python.org/3.9/faq/design.html)

출처: 

- [Real Python](https://realpython.com/) and official Python doc

목차

1. **[Memory Management](#memory-management)**
2. **[Global Interpreter Lock](#global-interpreter-lock)**

****

# Memory Management

출처: [Real Python](https://realpython.com/python-memory-management/), [Stackify](https://stackify.com/python-garbage-collection/#:~:text=The%20Python%20garbage%20collector%20has,a%20threshold%20number%20of%20objects.)

컴퓨터에서 프로그램이 실행될 때, OS에서 프로그램을 위해 할당하는 메모리는 fixed하다. 프로그램은 정해진 메모리 관리 알고리즘에 따라 주어진 메모리를 관리한다.

**CPython**

파이썬은 CPython이 베이스이다. CPython은 C로 만들어졌다.

CPython 외에도 다른 interpreter/compiler는 다음과 같다:
- IronPython - .NET
- Jython - JAVA
- MicroPython - 마이크로 컨트롤러

기본적으로 CPython이 하는 일은 다음과 같다.
1. .py에 적힌 코드를 bytecode로 compile 한다
2. .pyc (컴파일 된 코드)를 파이썬 가상 환경에서 실행한다

**파이썬의 object (int, list, etc)는 어떻게 관리가 될까?**

파이썬에서는 모든 object가 `PyObject`로 표현된다. 

`PyObject`는 C struct 이고:
- ob_refcnt: 이 object를 가르키고 있는 변수 갯수
- ob_type: 이 object의 type (int, list, etc)

와 같은 특성을 가지고 있다

`PyObject`의 `ob_refcnt` 특성이 0이 될 때, 가비지 콜렉터는 `PyObject`가 차지하고 있던 메모리를 다시 free 시킬 수 있다. 

*주의: 만약 object가 자기 자신을 reference 한다면?*
```python
class Foo(object):
    pass

# 'Foo' will be allocated in some place in the memory
a = Foo() # ob_refcnt of Foo = 1

# This will increment the ob_refcnt
a.obj = a # ob_refcnt of Foo = 2

# Will not deallocate the memory occupied by 'a' 
# because the ob_refcnt is never 0
del a # ob_refcnt of Foo = 1

# this is a 'reference cycle'
```
위와 같이 reference cycle이 생길 경우, `Foo` 가 차지하고 있는 메모리는 절대 비워지지 않는다. 

파이썬에서는 이것을 해결하고자 Generation garbage collector 도 같이 사용한다.

**Generation Garbage Collection**

2 가지 특징이 있다:
1. 가비지 콜렉터가 메모리 내에 모든 `object`를 track 한다. 이후 collection process에서 살아남은 `object`들은 다음 generation으로 넘어간다. 파이썬의 garbage collection process의 generation은 총 3번이다.
2. 각 generation 마다 threshold 가 있다. 이 threshold는 가비지 콜렉터가 track하는 `object`의 최대 갯수이다. 만약이 threshold를 넘어서게 되면, collection process가 시작되고 살아남은 `object`만 다음 세대로 넘어간다. 이 threshold는 개발자가 직접 바꿀 수 있다. *Instagram은 실제로 이 기능을 해제하여 서버를 10%가량 더 효율적으로 만들었다.*

**Global Interpreter Lock (GIL)**

메모리는 공유제이다. 메모리를 보호하는 알고리즘이 없다면 여러 프로세스가 같은 메모리 값을 읽고, 쓰고, 지우고 할 수 있다. 

하지만 이렇게 되면 race condition과 같은 문제점들이 발현다. 

이를 해결하는 방법은 여러가지인데 파이썬은 Global Interpreter Lock (GIL) 을 사용함으로써 메모리의 데이터를 보호한다.

파이썬의 GIL은 단일 Thread에게만 메모리 권한을 준다.  즉, 한 번에 한 Thread만이 파이썬 프로그램에 할당된 메모리 권한을 가지게 된다. 

**CPython Memory Management**

![image](https://files.realpython.com/media/memory_management.92ad564ec680.png)

위 그림과 같이 OS가 할당한 메모리 중 Python은 메모리를 크게 Object를 위한 메모리와 그외 메모리로 분할한다.

그리고 Object를 위한 메모리에 CPython의 object allocator가 할당된다.

이는 새 object 가 메모리에 할당되거나 삭제될 때마다 실행된다.

![image](https://files.realpython.com/media/memory_management_5.394b85976f34.png)

CPython 메모리 관리에는 크게 3 가지가 존재한다.

1. Arenas
    - 가장 큰 메모리 덩어리
    - OS가 메모리를 읽을 때 사용하는 블록과 연결된다     
    - Python은 Arena의 크기를 256 KB로 추정한다
    - eg. 256KB - 256KB - 256KB 단위로 OS가 읽는다

2. Pool
    - 가상 메모리
    - 4 KB
    - 더 작은 메모리 블록으로 이루어져 있다
    - Pool내에 모든 블록은 같은 "size class"다

3. Blocks
    - 8 bit 단위로 나뉘어진 "size class" 가 있다
    - eg. 데이터가 7 byte면 "size class"는 8이다, 데이터가 10이면 "size class"는 16이다.

**Pools**
- 같은 size class의 블록들로 구성된다
- 같은 size class를 담고 있는 pool들과 double-linked list를 형성한다
- 3 가지의 상태를 가진다:
    - `used` - 데이터를 저장할 블록을 가지고 있을 때
    - `full` - 모든 블록이 데이터로 가득 차 있을 때
    - `empty` - 데이터가 존재하지 않고 , 아무 size class로 구성된 블록들을 만들 수 있을 때

- `used`pools 은 새로운 객체가 저장 될 수 있는 block이 있는 모든 pool 리스트다 (저장되는 객체의 size는 block의 size class가 수용 가능 해야한다). 수용 가능한 블록을 찾을때 `used`pools 리스트에서 먼저 찾는다.

- `free`pools 는 모든 `empty` 상태의 pool을 기록한 리스트다.

- `full`에서 특정 블록을 free 할 경우, 그 pool의 상태는 `used`로 바뀐다. 

![image](https://files.realpython.com/media/memory_management_3.52bffbf302d3.png)

**Blocks**
- 3가지 상태가 있다:
    1. `untouched` - 할당되지 않은 메모리
    2. `free` - 할당 됐으나 CPython이 free 한 메모리
    3. `allocated` - 할당 된 메모리

- 위 그림과 같이, 각 pool 에는 자기 pool 내에 `free` 블록을 가르키는 포인터가 있다
- `free` 블록이 꼭 연속성을 가져야 하는 것은 아니다:
![image](https://files.realpython.com/media/memory_management_4.4a30dfa2d111.png)

-  `free` 블록을 가르키는 포인터는 `free` 블록들을 탐색할 수 있는 single linked list다

- 만약 필요한 메모리의 사이즈가 `free` 블록의 사이즈보다 클 경우, `untouched` 블록들을 사용한다

**Arena**

- 여러 개의 pool로 구성되어 있다
- double-linked 리스트다
- Arena내에 할당 가능한 pool의 갯수를 기준으로 정렬이 되어있다 (오름차순) 
- 오름차순인 이유?
    - CPython이 특정 메모리를 `free`한다는 것은 OS에게 그 메모리를 돌려준다는 뜻이 아니다. CPython은 메모리를 `free`한 이후에도 그 메모리를 계속 사용한다.
    <br>즉 Arena를 더 적게 사용하는 것이 전체적인 프로그램의 메모리를 더 적게 사용하는 것이다.
****

# Global Interpreter Lock
*[source](https://realpython.com/python-gil/#:~:text=The%20Python%20Global%20Interpreter%20Lock%20or%20GIL%2C%20in%20simple%20words,at%20any%20point%20in%20time.)*

- 간단히 말하면 mutex (lock) 이다. 단 하나의 thread만 Python Interpreter를 쓸 수 있게 하는 장치다
- CPU를 이용한 multi threaded 앱에서는 bottleneck이 될 수 있다
- 아무리 내 코드가 multi threaded용으로 짜여졌다고 하더라도, 실제로는 single threaded 앱처럼 실행이 된다

**왜 도입 됐는가?**

- 일단 Python GIL은 thread라는 개념이 존재하기 전에 도입됐다
- 파이썬 메모리 관리 특성 상 object에 대한 race condition이 생길 수 있는데, 이를 방지 하려면 일종의 lock이 필요했다
- object 단위로 lock을 도입하기에는 deadlock 문제가 생기고 성능이 저하 될 수 있어서 GIL을 도입했다.
- 가장 간단하고 효과적이었기 때문이다

**Parallel program은 파이썬으로 불가능한가?**

- Multi-threaded 말고 multi-process 방법으로 접근하면 앱을 parallel하게 짤 수 있다
- 혹은 다른 python interpreter를 사용하면 된다. GIL은 CPython 에만 존재하기 때문이다 (CPython이 Python의 베이스다)

****

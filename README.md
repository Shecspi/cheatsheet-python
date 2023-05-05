# Типы данных

## Классификация по типу
- Скалярные
  - `Числа`
  - `Логический тип`
  - `NoneType`
- Коллекции
  - Последовательности
    - `Строка | str`
    - [`Список | list`](https://github.com/Shecspi/cheatsheet-python#список--list)
    - [`Кортеж | tuple`](https://github.com/Shecspi/cheatsheet-python#кортеж--tuple)
    - `Числовая последовательности | range`
  - Множества
    - `Множество | set`
    - `Неизменяемое множество | frozenset`
  - Отображения
    - [`Словарь | dict`](https://github.com/Shecspi/cheatsheet-python#словарь--dict)

## Классификация по изменяемости
- Изменяемые
  - [`Список | list`](https://github.com/Shecspi/cheatsheet-python#список--list)
  - `Множество | set`
  - [`Словарь | dict`](https://github.com/Shecspi/cheatsheet-python#словарь--dict)
* Неизменяемые
  - `Числа`
  - `Логический тип`
  - `NoneType`
  - `Строка | str`
  - [`Кортеж | tuple`](https://github.com/Shecspi/cheatsheet-python#кортеж--tuple)
  - `Числовая последовательности | range`
  - `Неизменяемое множество | frozenset`

## Встроенные типы данных
### Список | List
Список - это упорядоченная изменяемая коллекция объектов произвольных типов и произвольной вложенности. 

Все описанные ниже методы изменяют оригинальный список на месте, не создавая новый, а также возвращают `None`.
```python
list[1] = ...              # Замена элемента
list[0:2] = ...            # Замена диапазона элементов

list.append(value)         # Вставка элемента в конец
list.extend([a, b, c])     # Вставка всех элементов итерируемого объекта в конец списка
list.insert(index, value)  # Вставляет элемент value на позицию index

list.pop()                 # Удаление последнего или указанного элемента списка
list.remove(value)         # Удаление элемента по значению (первое совпадение)
list.clear()               # Очищает список

list.sort()                # Сортировка в прямом порядке
list.reverse()             # Сортировка в обратном порядке
list.count(value)          # Подсчёт количества вхождений элемента в список
list.index(value)          # Поиск индекс элемента
```

Метод `copy()` создаёт новый список.
```python
list.copy()  # Копирует список и возвращает новый
```

`list.sort()` и `sorted(list)` делают одно и то же - сортируют список. Но метод `sort()` делает это на месте и ничего не возвращает, а функция `sorted()` создаёт и возвращает новый список, не меняя оригинальный.
```python
symbols = ['e', 'd', 'a', 'c', 'b']
sorted_symbols = sorted(symbols)  # Создание нового отсортированного списка
symbols.sort()  # Сортировка изначального списка на месте

# Значения списков одинаковые, но это разные объекты
print(symbols == sorted_symbols)  # True
print(symbols is sorted_symbols)  # False
```

### Кортеж | Tuple
Кортеж - это упорядоченная неизменяемая коллекция объектов произвольных типов и произвольной вложенности. Потребляет меньше памяти, чем список той же длины, а также является более эффективным, чем список.
* Если `t` это кортеж, то `tuple(t)` возвращает ссылку на `t`, a `list(l)` создаёт копию списка `l`.
* Для кортежа выделяется ровно столько памяти, сколько требуется. Для списка память выделяется с запасом.
* Ссылка на элементы кортежа хранятся в самом кортеже, а список хранит указатель на массив ссылок, расположенный в другом месте.
```python
list.count(value)  # Подсчёт количества вхождений элемента в список
list.index(value)  # Поиск индекс элемента
```

Несмотря на то, что кортеж - это неизменяемый тип данных, его элементы могут указывать на изменяемый тип. В таком случае в случае изменения объекта изменится и кортеж.
```python
a = (10, 'alpha', [1, 2])
b = (10, 'alpha', [1, 2])
print(a == b)  # True

b[-1].append(99)
print(a == b)  # False, так как изменили изменяемый элемент в кортеже
```

### Словарь | Dict
Словарь - это упорядоченная изменяемая коллекция объектов произвольных типов и произвольной вложенности. Является высокооптимизированным типом данных, основанным на хэш-таблицах.

```python
dict[key]        # Доступ по ключу
dict[key] = ...  # Изменение элемента словаря на месте

key in dict      # Проверка наличия ключа в словаре
dict.keys()      # Возвращает объект представления со всеми ключами словаря
dict.values()    # Возвращает объект представления со всеми значениями словаря
dict.items()     # Возвращает кортеж с парами ключ-значение словаря

dict.copy()      # Копирует словарь
dict.clear()     # Очищает словарь
dict.update()    # Обновляет или дополняет словарь
dict.get(key)    # Возвращает значение по ключу
dict.pop(key)    # Удаляет указанный ключ из словаря и возвращает его значение

dict1 | dict2    # Объединяет два словаря, не изменяя их самих
dict1 =| dict2   # Объединяет два словаря и записывает новый в dict1
```

## Расширенные типы данных
### Именованный кортеж | Named tuple
```python
from collections import namedtuple

employee = namedtuple('employee', ['name', 'age'])
Bob = employee(name='Bob', age=33)
print(Bob.name, Bob[1])  # Возможен доступ по имени и смещению
```

---
---

### Распаковка коллекций | Unpacking
```python
print(*(33.44, 55.66))                        # Распаковка кортежа
print(*[33.44, 55, 66])                       # Распаковка списка
print(*{33.44, 55.66})                        # Распаковка  множества
print(*{'lat': 33.44, 'lon': 55.66}.items())  # Распаковка словаря
print(*'string')                              # Распаковка строки

# Распаковка кортежа для выборки лишних элементов
# *rest может находиться не только в конце, но и в начале и середине
a, b, *rest = range(5)  # rest = [2, 3, 4]
a, *rest, b, c = range(5)  # rest = [1, 2]

# Распаковка кортежа для использования в функции
def foo(a, b, *rest):
    return a, b, rest

coordinates = (33.44, 55.66)
foo(*coordinates)  # (33.44, 55.66, ())
foo(*coordinates, *coordinates, 1, 2, 3)  # (33.44, 55.66, (33.44, 55.66, 1, 2, 3))

# Распаковка для определения списка, кортежа или коллекции
tpl = *range(5), 5  # (0, 1, 2, 3, 4, 5)
lst = [*range(5), 5]  # [0, 1, 2, 3, 4, 5]
st = {*range(5), 5}  #{0, 1, 2, 3, 4, 5}

# Распаковка вложенных кортежей
cities = [
    ('Moscow', 'Russia', (55.755864, 37.617698)),
    ('Minsk', 'Belarus', (53.902735, 27.555696))
]
for name, _, (lat, lon) in cities:
    print(f'{name:8} | {lat:8.4f} | {lon:8.4f}')
```

---
---

### Списковое включение | List comprehension
Создаваемый список полностью попадает в память.  
**Пример 1:**
```python                                                                                  
sizes = ['S', 'M', 'L']                                                                                         
print([size for size in sizes])
```
`>>> ['S', 'M', 'L']`

**Пример 2**:
```python
colors = ['black', 'white']                                                                                     
sizes = ['S', 'M', 'L']                                                                                         
t_shirts = [(color, size) for color in colors for size in sizes]                                                
print(t_shirts)
```

`>>> [('black', 'S'), ('black', 'M'), ('black', 'L'), ('white', 'S'), ('white', 'M'), ('white', 'L')]`

### Генераторное выражение | Generator expression
Отдаёт элементы по одному, применяя протокол итератора, а не строит список полностью. Это дешевле по памяти, чем списковое включение.
```python
colors = ['black', 'white']                                                                                     
sizes = ['S', 'M', 'L']                                                                                         
for t_shirts in (f'{color} {size}' for color in colors for size in sizes):                                      
    print(t_shirts) 
```

```
>>> black S
    black M
    black L
    white S
    white M
    white L
```

### Словарное включение | Dictionary comprehension
Создаёт объект dict, порождая пары key:value из итерируемого объекта.
```python
some_codes = [
    (1, 'Moscow'),
    (2, 'SPB'),
    (3, 'Kazan')
]
cities = {str(number): city.upper() for number, city in some_codes}
print(cities)
```

---
---

### Сопоставление с образцом | match/case
```python
# Простое сопоставление
message = 'hello'
match message:
    case 'hello':
        print('Hello')
    case 'wolrd':
        print('World')
    case _:
        print('Error')

# Сопоставление с распаковкой
# Проверка сработает только при совпадении количества элементов
message = ['hello', 'world', 1]
match message:
    case ['hello', second, third]:
        print(second, third)

# Распаковка вложенных кортежей и проверка по условию
# Проверка сработает только при совпадении количества элементов
# (включая вложенные) и корректности условия
area = ('Moscow', 'Russia', (55.755864, 37.617698))
match area:
    case [city, country, (lat, lon)] if lat >= 55:
        print(f'{city:7} | {lat:9.4f} | {lon:9.4f}')
 
# Проверка типов при сопоставлении
# Проверка сработает только при совпадении количества элементов и их типов
area = ('Moscow', 'Russia', (55.755864, 37.617698))
match area:
    case [str(city), *_, (float(lat), float(lon))]:
        print(f'{city:7} | {lat:9.4f} | {lon:9.4f}')
```

---
---
# Итерируемый объект
**Итерируемый объект** - это объект, реализующий методы `__iter__` или `__getitem__` (который не рекомендуется к использованию) и возвращающий итератор.  
**Итератор** - это объект, реализующий методы `__iter__` (возвращает `self`) и `__next__` (возвращает следующий доступный элемент или исключение `StopIteration`.  
Итераторы очень активно применяются в Python, например, цикл `for` для перебора объектов коллекций взаимодействует не с самим объектом, а с его итератором через неявный вызовом функции `iter()`.
Реализация аналога цикла `for`:
```python
lst = ['value1', 'value2', 'value3']

# Получение итератора от итерируемого объекта
it = iter(lst)
    
while True:
  try:
      print(next(it))
  except StopIteration:
    del it
    print('Окончание итерации')
```

Простой пример реализации итерируемого объекта и итератора:
```python
class FindAllWords:
    """
    Это итерируемый объект, который создаёт и возвращает итератор.
    """
    def __init__(self, text):
        self.text = text
        self.words = text.split()
    
    def __repr__(self):
        return f'FindAllWords ("{self.text}")'
    
    def __iter__(self):
        return FindAllWordsIterator(self.words)


class FindAllWordsIterator:
    """
    Это итератор, возвращающий значения по одному за раз.
    """
    def __init__(self, words):
        self.words = words
        self.index = 0
        
    def __next__(self):
        try:
            word = self.words[self.index]
        except IndexError:
            raise StopIteration
        self.index += 1
        return word
    
    def __iter__(self):
        return self


words = FindAllWords("Проверка работы созданного мною кастомного итератора")
print(words)
for word in words:
    print(word)
```
Такого же результата можно добиться с помощью ключевого слова `yield`, благодаря чему код сократиться и не будет необходимости отдельно описывать итератор.
```python
class FindAllWords:
    def __init__(self, text):
        self.text = text
        self.words = text.split()
    
    def __repr__(self):
        return f'FindAllWords ("{self.text}")'
    
    def __iter__(self):
        """
        Метод __init__ является генераторной функцией,
        которая возвращает значения по одному за раз.
        Поэтому результат получается аналогичным первому примеру
        с отдельной реализацией итерируемого объекта и итератора.
        """
        for word in self.words:
            yield word


words = FindAllWords("Проверка работы созданного мною кастомного итератора")
print(words)
for word in words:
    print(word)
```
Метод `__iter__` можно ещё сократить, используя `iter()`, который возвращает итератор переданного ему объекта.  
А также возвожно использовать конструкцию `yield from`.
```python
def __iter__(self):
  return iter(self.words)
# Или
def __iter__(self):
  yield from self.words
```

# Менеджеры контекста
Менеджер контекста - это объект, реализующий dunder-методы `__enter__()` и `__exit__()`, выполнение которых гарантируется вне зависимости от исполняемого кода (даже в случае исключения). Менеджеры контекста являются упрощением конструкции `try/finally`. Контекстные методы удобно применять там, где необходимо выполнить какое-либо действие вне зависимости от результата выполнения программы (например, закрыть файл или базу данных).
```python
class MyContextManager:
    def __enter__(self):
        print('Всегда выполняется вначале')
        # Наличие оператора `return` не обязательно, тогда возвращаемое значение будет `None`.
        # Возвращаемое этим методом значение будет присвоено переменной, указанной после `as`.
        return self
    
    def __exit__(self, exc_type, exc_value, traceback):
        print('Всегда выполняется в конце')


with MyContextManager() as cm:
    print('Основной код программы')
    # Следующий код вызовет исключение ZeroDivision, но метод __exit__() выполнится в любом случае
    #1/0

# Конструкция `with` не создаёт локальной области видимости,
# поэтому переменная `cm` остаётся доступной вне блока `with`
print(cm)  # <__main__.MyContextManager object at 0x...>
```

---
---
# Классы данных
### collections.namedtuple
`collections.namedtuple` - это фабрика, порождажющая подклассы `tuple`, дополненные возможностью задавать имена полей, имя класса и информативный метод `__repr__`. Экземпляры этого класса потребляют столько же памяти, сколько и кортежи, так как имена хранятся в определении класса.
```python
from collections import namedtuple

# Первый параметр - имя класса
# второй - перечисление полей в виде строки с пробелами или итерируемого объекта
# `defaults` определяет значения по-умолчанию в порядке справа налево
City = namedtuple('City', 'name country coordinates', defaults=[(35.689722, 139.691667)])
tokyo = City('Tokyo', 'Japan')

print(tokyo)  # Выведет "City(name='Tokyo', country='Japan', coordinates=(35.689722,  139.691667))"

# К полям можно обращаться по имени
print(tokyo.name, tokyo.country)  # 'Tokyo Japan'

# И по смещению
print(tokyo[0], tokyo[1])  # 'Tokyo Japan'

# _fields возвращает кортеж, содержащий имена полей
print(City._fields)  # ('name', 'country', 'coordinates')

# _field_defaults возвращает словарь со значениями по-умолчанию
print(City._field_defaults)  # {'coordinates': (35.689722, 139.691667)}

# _asdict() возвращает все поля в виде словаря
print(tokyo._asdict())  # {'name': 'Tokyo', 'country': 'Japan', ... }
```

### typing.NamedTuple
`typing.NamedTuple` - типизированныя версия класса `collections.namedtuple`
```python
from typing import NamedTuple

class City(NamedTuple):
    name: str
    country: str = 'Russia'
    coordinates = (35.689722, 139.691667)

# NamedTuple не имеет методов, помимо тех, что генерирует collections.namedtuple,
# а также унаследованных от tuple. Единственное различие -
# наличие атрибута __annotations__, который возвращает типы всех полей класса.
print(City.__annotations__)  # {'name': <class 'str'>, 'country': <class 'str'>}

# Поле `name` становится атрибутом экземпляра и для него заводится аннотация
print(City.name)  # │_tuplegetter(0, 'Alias for field number 0')

# Поле `country` становится атрибутом экземпляра со значением по-умолчанию
# и для него заводится аннотация
print(City.country)  # _tuplegetter(1, 'Alias for field number 1')

# Поле `coordinates` является обычным атрибутом класса без аннотации
print(City.coordinates)  # (35.689722, 139.691667)

# Аттрибуты класса не допускают изменения, так как NamedTuple -
# это наделённый дополнительными возможностями кортеж
city = City('Moscow')
city.name = 'Kazan'  # AttributeError: can't set attribute
```

### dataclass
Все атрибуты датакласса являются изменяемыми, в отличие от `typing.NamedTuple` и `collections.namedtuple`.
```python
from dataclasses import dataclass

@dataclass
class City:
    name: str
    country: str = 'Russia'
    coordinates = (35.689722, 139.691667)

city = City('Moscow')
print(City.__annotations__)  # {'name': <class 'str'>, 'country': <class 'str'>}

# Поле `name` имеет аннотацию, но не становится атрибутом класса.
# При этом в экземпларах класса оно будет, и его можно читать и записывать.
print(City.name)     # AttributeError: type object 'City' has no attribute 'name'
city.name = 'Kazan'  # Поле `name` доступно для редактирования
print(city)          # City(name='Kazan', country='Russia')

# Поле `country` имеет аннотацию и становится атрибутом экземпляра
print(City.country)  # Russia

# Поле `coordinates` является обычным атрибутом класса без аннотации
# Его не будет в экземплярах класса, но оно будет доступно как атрибут класса
print(City.coordinates)  # (35.689722, 139.691667)
print(city)              # City(name='Kazan', country='Russia')
print(city.coordinates)  # (35.689722, 139.691667)
```

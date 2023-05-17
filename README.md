# Оглавление
1. [Типы данных](Типы%20данных.md)
	1. [Классификация типов](Типы%20данных.md#Классификация-типов-данных)
	2. [Встроенные типы](Типы%20данных.md#Встроенные-типы-данных)
	3. [Расширенные типы](Типы%20данных.md#Расширенные-типы-данных)
	4. [Распаковка коллекций](Типы%20данных.md#Распаковка-коллекций)
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

# Менеджер контекста
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
    1/0

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

# Типы данных

## Классификация по типу
- Скалярные
  - `Числа`
  - `Логический тип`
  - `NoneType`
- Коллекции
  - Последовательности
    - `Строка | str`
    - [`Список | list`](https://github.com/Shecspi/cheatsheet-python/edit/master/README.md#список--list)
    - [`Кортеж | tuple`](https://github.com/Shecspi/cheatsheet-python/edit/master/README.md#кортеж--tuple)
    - `Числовая последовательности | range`
  - Множества
    - `Множество | set`
    - `Неизменяемое множество | frozenset`
  - Отображения
    - [`Словарь | dict`](https://github.com/Shecspi/cheatsheet-python/edit/master/README.md#кортеж--tuple)

## Классификация по изменяемости
- Изменяемые
  - [`Список | list`](https://github.com/Shecspi/cheatsheet-python/edit/master/README.md#список--list)
  - `Множество | set`
  - [`Словарь | dict`](https://github.com/Shecspi/cheatsheet-python/edit/master/README.md#кортеж--tuple)
* Неизменяемые
  - `Числа`
  - `Логический тип`
  - `NoneType`
  - `Строка | str`
  - [`Кортеж | tuple`](https://github.com/Shecspi/cheatsheet-python/edit/master/README.md#кортеж--tuple)
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

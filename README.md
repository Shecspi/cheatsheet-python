## Типы данных
### Кортеж | Tuple
Неизменяемый тип данных. Потребляет меньше памяти, чем список той же длины,
а также является более эффективным, чем список:
* Если `t` это кортеж, то `tuple(t)` возвращает ссылку на `t`,
a `list(l)` создаёт копию списка `l`.
* Для кортежа выделяется ровно столько памяти, сколько требуется.
Для списка память выделяется с запасом.
* Ссылка на элементы кортежа хранятся в самом кортеже,
а список хранит указатель на массив ссылок, расположенный в другом месте.
```python
# Кортеж
cities = ('Moscow', 'SPB', 'Kazan')

# Распаковка кортежа
city, year = ('Moscow', 2023)

# Распаковка кортежа через оператор форматирования %
visited_cities = [('Moscow', 2023), ('SPB', 2022), ('Kazan', 2021)]
for city in visited_cities:
    print('%s / %s' % city)

# Распаковка кортежа в цикле
for city, year in visited_cities:
    print(city, year)

# Распаковка через оператор *
t = (20, 8)
print(divmod(*t))

# Выборка лишних элементов
a, b, *rest = range(10)
print(a, b, rest)

```
Но если какая-то ссылка в кортеже указывает на изменяемый объект, то значение кортежа тоже может измениться.
```python
a = (10, 'alpha', [1, 2])
b = (10, 'alpha', [1, 2])
print(a == b)  # True

b[-1].append(99)
print(a == b)  # False, так как изменили изменяемый элемент в кортеже
```




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
___
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

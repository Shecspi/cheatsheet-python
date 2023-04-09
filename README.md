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

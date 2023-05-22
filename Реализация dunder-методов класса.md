```python
from array import array
import math


class Vector2d:
    typecode = 'd'

    @property
    def x(self):
        return self.__x

    @property
    def y(self):
        return self.__y


    def __init__(self, x: float, y: float) -> None:
        self.__x = x
        self.__y = y

    def __repr__(self) -> str:
        """
        Возвращает строку, представляющую объект в виде, удобном для разработчиков.

        Например:
            Vector2d(2.0, 3.0)
        """
        return '{}({!r}, {!r})'.format(type(self).__name__, *self)

    def __str__(self) -> str:
        """
        Возвращает строку, представляющую объект в виде, удобном для пользователя.

        Например:
            (2.0, 3.0)
        """
        return str(tuple(self))

    def __bytes__(self):
        """
        Возвращаает байтовое представление экземпляра класса.
        """
        return (bytes([ord(self.typecode)]) + bytes(array(self.typecode, self)))

    def __eq__(self, other):
        """
        Реализует поведение оператора `==`.
        """
        return tuple(self) == tuple(other)

    def __abs__(self):

        return math.hypot(self.x, self.y)

    def __bool__(self):
	    """
	    Реализует булевые операции.
	    """
        return bool(abs(self))
    
    def __format__(self, format_spec=''):
        """
        Реализует логику работы встроенной функции `format()` по отношению к экземпляру класса.
        """
        components = (format(c, format_spec) for c in self)
        return '({}, {})'.format(*components)

    def __iter__(self):
        """
        Делает метод итерируемым.
        """
        return (i for i in (self.x, self.y))

    def __hash__(self):
        """
        Делает объект хэшируемым.
        Для этого необходимо гарантированность неизменяемости `x` и `y` - через @property.
        """
        return hash((self.x, self.y))


vector = Vector2d(2.0, 3.0)

print(vector.x, vector.y)  # 2.0 3.0

x, y = vector
print(x, y)  # 2.0 3.0

# Тестирование метода __str__()
print(vector)  # (2.0, 3.0)

# Тестирование метода __repr__()
print(repr(vector))  # Vector2d(2.0, 3.0)

# Тестирование метода __bytes__()
print(bytes(vector))  # b'd\x00\x00\x00\x00\x00\x00\x00@\x00\x00\x00\x00\x00\x00\x08@'

# Тестирование метода __eq__()
print(vector == eval(repr(vector)))  # True

# Тестирование метода __abs__()
print(abs(vector))  # 3.605551275463989

# Тестирование того, что аттрибуты `x` и `y` доступны только на чтение
# vector.x = 5.0  # AttributeError: property 'x' of 'Vector2d' object has no setter

# Тестирование метода __hash__()
print(hash(vector))  # 8409376899596376432

```
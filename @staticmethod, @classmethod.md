### @staticmethod
Изменяет метод таким образом, что он не получает в первом аргументе специального, только реально переданные данные. Статический метод - это просто обычная функция, определённая в теле класса, но не имеющая доступа к данным этого класса.

### @classmethod
Определяет метод на уровне класса, а не отдельного экземпляра, и изменяет способ вызова метода таким образом, что в качестве первого аргумента передаёт в метод сам класс, а не его экземпляр.

```python
class Demo:
    def regular_method(*args):
        return args

    @classmethod
    def class_method(*args):
        return args

    @staticmethod
    def static_method(*args):
        return args


print(Demo.regular_method('regular'))  # ('regular',) - только переданные аргументы
print(Demo.class_method('class'))  # (<class '__main__.Demo'>, 'class') - класс и переданные аргументы
print(Demo.static_method('static'))  # ('static',) - только переданные аргументы

demo = Demo()
print(demo.regular_method('regular'))  # (<__main__.Demo object at 0x7f11a8f16f90>, 'regular') - экземпляр класса и переданные аругемнты
print(demo.class_method('class'))  # (<class '__main__.Demo'>, 'class') - класс и переданные аргументы
print(demo.static_method('static'))  # ('static',) - только переданные аргументы

```
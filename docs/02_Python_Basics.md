# Python Basics

## Какой Python язык?

- Динамическая типизация, но можно статическую типизацию сделать с помощью mypy
- Мультипарадигмальный, общего назначения с верхнеуровневым и низкоуровневым апи
- Компилируемый - компилируется в байт-код - `.pyc`
    - Интерпретируемость - это ложь

## Типы данных

| Immutable | Mutable |
|-----------|---------|
| `None`    | `list`  |
| `bool`    | `set`   |
| `int`     | `dict`  |
| `float`   |         |
| `str`     |         |
| `tuple`   |         |

### ` == ` vs `is`

- ` == ` - по значению / по методу `__eq__`
- `is` - по адресу в памяти: `id(a) == id(b)`
    - Для чисел и строк это равносильно `==`, потому что [Intering](05_Память.md)

### Еще о Immutable

#### Что будет при изменении строки/тьюпла по индексу

- Ошибка `TypeError`, напр. `TypeError: 'str' object does not support item assignment`

#### В чем плюс иммутабельных типов

- Быстрее
- Меньше памяти жрут
- Хешируемы - можно использовать в словарях/сетах

#### Как сделать класс - хешируемым

- Реализовать `__hash__`, `__eq__`

### copy

- `copy` - не дип копирование
- `deepcopy` - дип-копирование, включая списки и дикты

## Скоуп переменных aka LEGB

- LEGB: Local, Enclosing, Global, Built-in

### Local

- Переменная локальная только внутрии функции/класса

```python
def f():
    x = 1
    print(x)  # x = 1
```

### Enclosing

```python
def f():
    x = 1

    def g():
        print(x)  # x = 1

    g()
```

### Global

```python
x = 1


def f():
    print(x)  # x = 1
```

#### `global`

```python
x = 1


def f():
    global x
    print(x)  # x = 1
    x = 2


f()
print(x)  # x = 2
``` 

### Built-in

```python
__name__  # '__main__'
__name__ = 'test'
print(__name__)  # 'test'
```

## Exceptions / Эксепшены / Ошибки

### `BaseException` vs `Exception`

- `BaseException` - для builtin-ошибок, в целом не должны использоваться в коде
- `Exception` - базовый класс для ошибок, ловить/пользоваться нужно ими

## Декораторы

```python
import datetime
import functools


def timeit(func):
    @functools.wraps(func)
    def wrap(*args, **kwargs):
        start = datetime.datetime.now()
        res = func(*args, **kwargs)
        end = datetime.datetime.now()
        print(end - start)
        return res

    return wrap
```

### Декоратор с параметрами

- Просто еще один слой враппинга:

```python
def deco_w_params(param):
    def timeit(func):
        @functools.wraps(func)
        def wrap(*args, **kwargs):
            start = datetime.datetime.now()
            res = func(*args, **kwargs)
            end = datetime.datetime.now()
            print(end - start)
            return res

        return wrap

    return timeit
```

## Итераторы / генераторы / итерируемый объект

- Итератор: `__iter__`, `__next__`
- Генератор - объект, лениво отдающий свои данные
- Итерируемый объект - то что в for можно сунуть

## Context Manager

### Как сделать свой?

- `@contextmanager`
- `class`: `__enter__`, `__exit__`

## Стандартная библиотека

- std: collections / itertools / etc.

## Материалы

- [Хитрый питон: Mutable и Immutable типы данных в python](https://www.youtube.com/watch?v=hSdZxrpTkh0)
- [Хитрый питон: Глобальные и локальные переменные в python](https://www.youtube.com/watch?v=9YBcJYEqXho)
- [Лучший курс по Python 3: Какой Python язык?](https://www.youtube.com/watch?v=rc0tJaPleTg&list=PLbr8rVGhPD0WQgO97Ao67Q-QVuSbm_Zpz&index=4)
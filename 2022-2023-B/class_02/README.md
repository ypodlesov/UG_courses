# Теоретико числовые алгоритмы. Часть 2.

## Диофантовы уравнения

Диофантово уравнение - это уравнение относительно целых чисел $x$, $y$ вида

$$ 
a \cdot x + b \cdot y = c 
$$

где $a$, $b$, $c$ - заданные целые числа.

### Вырожденный случай

**Вырожденный случай** возникает, когда $a = b = 0$. Тогда если $c = 0$, то
уравнение имеет бесконечно много решений, иначе ни одного.

### Нахождение одного решения

Очевидное утверждение, диофантово уравнение имеет решение тогда и только тогда,
когда $gcd(a, b)$ $\mid$ $c$. 

Следовательно: 

$$
a \cdot x_g + b \cdot y_g = \gcd(a, b)
$$

$$
a \cdot x_g \cdot (c / \gcd(a, b)) + b \cdot y_g \cdot (c / \gcd(a, b)) = c
$$

То есть 

$$
x_0 = x_g \cdot (c / \gcd(a, b)) \text{ и } y_0 = y_g \cdot (c / \gcd(a, b))
$$

является одним из решений диофантового уравнения. Найти его можно при помощи
расширенного алгоритма евклида, описанного раннее.

### Нахождение всех решений

Если диофантово уравнение имеет решение, то их бесконечно много. Поэтому
зачастую в задаче на нужные решения накладывают дополнительные условия.
Например, найти все решения из нужного сегмента.

**Утверждение:** Пусть $k$ - произвольное целое число. 
Тогда $(x_0 + k \cdot b / g$, $y_0 - k \cdot a / g)$ - решение тогда и только тогда, когда
$(x_0,$ $y_0)$ - решение. 

## Функция Эйлера

**Функция Эйлера** $\phi(n)$ - количество чисел от 1 до $n$, взаимно простых с
$n$. 

Например, 

$$\phi(1) = 1$$

$$\phi(2) = 1$$

$$\phi(3) = 2$$

$$\phi(4) = 2$$ 

$$\phi(5) = 4$$

Приведём важные свойтва функции Эйлера:

1. Если $p$ - простое числе, то $\phi(p) = p - 1$
2. Если $p$ - простое, $a$ - натуральное число, то $\phi(p^a) = p^a - p^{a-1}$
3. Если $a$ и $b$ - взаимно простые числа, то $\phi(ab) = \phi(a)\phi(b)$

Попробуйте, используя эти три свойства, написать реализацию вычисления функции
Эйлера.

**Теорема Эйлера:** Если $a$ и $m$ взаимно просты, 
то $a^{\phi(m)} \equiv 1 \mod(m)$

## Бинарное возведение в степень

Поставим задачу вычислить $a^n$, где $a$ - произвольное число, $n$ - целое число.
Наивное решение - просто $n$ раз умножить 1 на число $a$. Данное решение очевидно
имеет сложность $O(n)$. 

Но есть и более оптимальный алгоритм, основанный на следующем утверждении:

**Утверждение:** Если $n$ - четно, то $a^n = (a^{n/2})^2$

Приведём псевдокод данного алгоритма:

```
binpow(a, n)
    if (n == 0)
        return 1
    if (n % 2 == 1)
        return binpow(a, n-1) * a
    else 
        b = binpow(a, n/2)
        return b * b
```

Попробуйте подумать, как можно реализовать данный алгоритм в нерекурсивном виде.

## Обратный элемент в кольце по модулю

Задача ставится следующим образом: даны целые числа $a$ и $m \in \mathbb{N}$.

Требуется найти число $b$ такое, что $a \cdot b \equiv 1 \mod(m)$

При решении данной задачи можно пойти по двум основным путям:

1. Расширенный алгоритм Евклида
2. Бинарное возведение в степень

Как оба этих решения можно реализовать, предлагается подумать самостоятельно.

## Комбинаторик

В этом разделе рассмотрим основные комбинаторные объекты. 

### Числа Фибоначчи

Числа Фибоначчи определяются так: 

Если $n > 2$, то: 

$$
F(n) = F(n-1) + F(n-2)
$$

Начальные значения:

$$
F(0) = 0, \text{ } F(1) = 1
$$

С числами Фибоначчи связаны два утверждения: 

1. **Теорема Цекендорфа:** каждое положительно число можно единственным образом
   представить в виде суммы чисел Фибоначчи так, чтобы в этом представлении не
   оказалось двух соседних.
2. **Период Пизано:** последняя / последние две / последние три / последние
   четыре цифры числа Фибоначчи повторяются с периодичностью 60/300/1500/15000
   соответственно.  

### Числа Каталана

$n$-е число Каталана определяется как: 
$$Cat(n) = (C^{n}_{(2 \cdot n)})(n+1) \text{; } Cat(0) = 1$$

Числа Каталана можно вычислять рекурсивно: 

$$Cat(n+1) = \frac{(2n + 2) \cdot (2n + 1)}{(n + 2) \cdot (n + 1)} \cdot Cat(n)$$

Наиболее интересные приложения: 

1. $Cat(n)$ - количество различных двоичных деревьев с $n$ вершинами.
2. $Cat(n)$ - количество правильных скобочных последовательностей из $n$ пар
   скобок.
3. $Cat(n)$ - количество свособов триангуляции выпуклого многоугольника с $n + 2$ сторонами.

# Урок 1. Расчет вероятности случайных событий

## Теория
**Случайное событие** - это событие, которое при определенных условиях может произойти либо не произойти.

Случайные события могут быть:
- **достоверными** - если в результате испытания они обязательно происходят
- **невозможными** - если в результате испытания они никогда не могут произойти
<br><br>
- **зависимыми** - появление одного события, не влияет на появление другого
- **независимыми** - когда появление одного события влияет на появление другого
<br><br>
- **совместными** - появление одного исключает появление другого
- **несовместными** - появление одного не исключает появления другого

### Вероятность
**Относительная частота** - эксперементальная характеристика, полученная эмпирически, при небольшом количестве испытаний.

$\displaystyle W(A) = \frac{m}{n}$

**Статистическая вероятность** - так же экспериментальная характеристика, но, в отличии от ОЧ, полученная на большом количестве испытаний

$\displaystyle P(A) = \frac{m}{n}$

**Классическое определение вероятности** - отношение числа элементарных исходов, благоприятствующих данному событию, к числу всех равновозможных исходов опыта, в котором оно может появиться (расчетная величина, применяется если заранее известны все вероятные исходы и они равновозможны)

$\displaystyle P(A) = \frac{m}{n}$

(здесь в формулах *m* - благоприятствующие исходы, *n* - общее количество испытаний)

### Комбинаторика
**Сочетания** - набор, состоящий из *k* элементов, выбранных из множества, содержащего *n* различных элементов. Порядок элементов не важен.

$\displaystyle C_n^k = \frac{n!}{k!(n-k)!}$

**Размещения** - размещения из *k* элементов, выбранных из множества *n* – это такие комбинации, которые отличаются либо самими элементами, либо порядком их расположения.

$\displaystyle A_n^k = \frac{n!}{(n-k)!}$

**Перестановки** - комбинации из *n* элементов, отличающиеся их порядком. Порядок элементов важен.

$\displaystyle P_n = n!$

---
**Задача 01.** Сколькими способами можно выбрать из колоды, состоящей из 36 карт, 4 карты?

$\displaystyle C_n^k = \frac{n!}{k!(n-k)!} = \frac{36!}{4!(36-4)!} = \frac{33 \cdot 34 \cdot 35 \cdot 36}{2 \cdot 3 \cdot 4} = 58905$

(факториал 32 сократился)

```
def comb(n, k):
    res = np.math.factorial(n) / (np.math.factorial(k) * np.math.factorial(n - k))
    return res

comb(36, 4)
```
---
**Задача 02.** В магазине 20 покупателей. Сколькими способами они могут образовать очередь из 5 человек?

$\displaystyle A_n^k = \frac{n!}{(n-k)!} = \frac{20!}{(20-5)!} = 16 \cdot 17 \cdot 18 \cdot 19 \cdot 20 = 1860480$

```
def arrangements(n, k):
    res = np.math.factorial(n) / np.math.factorial(n - k)
    return res

arrangements(20, 5)
```
---
**Задача 03.** Сколькими способами 5 покупателей могут образовать очередь?

$P_n = n! = 5! = 120$

```
def permutations(n):
    res = np.math.factorial(n)
    return res

permutations(5)
```
---
**Задача 04.** Из колоды, состоящей из 36 карт, случайным образом выбраны 5. Сколькими способами можно выбрать эти карты так, чтобы  среди них оказалось  2 туза? (ровно 2 туза)

Берем множество сочетаний тузов:

$\displaystyle C_n^k = \frac{n!}{k!(n-k)!} = \frac{4!}{2!(4-2)!} = \frac{3 \cdot 4}{2} = 6$

Теперь берем множество сочетаний без тузов:

$\displaystyle C_n^k = \frac{n!}{k!(n-k)!} = \frac{32!}{3!(32-3)!} = \frac{30 \cdot 31 \cdot 32}{6} = 4960$

Теперь найдем все возможные сочетания множества сочетаний тузов и множества сочетаний не тузов:

$C = 6 * 4960 = 29760$

---
**Задача 05.** Из колоды 36 карт случайным образом берут 5 карт. Найти вероятность того, среди 5 карт будет ровно 2 туза.

Мы знаем, что сочетаний из 5 карт с двумя тузами - 29 790 (из прошлой задачи). Значит здесь нужно просто посчитать вероятность извлечь любую из них из всех возможных сочетаний 5 карт из 36:

$\displaystyle C_n^k = \frac{n!}{k!(n-k)!} = \frac{36!}{5! \cdot 31!} = 376992$

Тогда вероятность получить комбинацию с 2 тузами равна:

$\displaystyle P(A) = \frac{m}{n} = \frac{29760}{376992} = 0.789$

### Вероятности зависимых и независимых событий

Вероятность одновременного появления двух независимых событий:

$\displaystyle P(AB) = P(A) \cdot P(B)$

Вероятность одновременного появления двух зависимых событий:

$\displaystyle P(AB) = P(A) \cdot P(B|A)$

($P(B|A)$ - читается как "вероятность наступления B, если A уже наступило")

---
**Задача 06.** В ящике лежат 3 фиолетовых и 2 черных шара. Найти вероятность, что подряд вытащат фиолетовый и черный шар.

Найдем вероятность вытащить первым фиолетовый шар (A):

$\displaystyle P(A) = \frac{m}{n} = \frac{3}{5}$

Теперь найдем вероятность вытащить черный шар, если первым удалось взять фиолетовый (B):

$\displaystyle P(B) = \frac{m}{n} = \frac{2}{4} = \frac{1}{2}$

Наконец, определим вероятность вытащить сначала фиолетовый шар, потом черный (AB):

$\displaystyle P(AB) = P(A) \cdot P(B|A) = \frac{3}{5} \cdot \frac{1}{2} = \frac{3}{10}$

---
### Вероятности совместных и несовместных событий (на примерах)

Например найдем шанс выпадения одновременно 1 и 2 на одной игральной кости:

Сначала определим вероятность выпадения 1 (A):

$\displaystyle P(A) = \frac{m}{n} = \frac{1}{6}$

Теперь, при выпадении 1, определим вероятность получить 2 (B|A):

$\displaystyle P(B|A) = 0$

Таким образом, вероятность одновременного наступления этих событий (AB):

$\displaystyle P(AB) = P(A) \cdot P(B|A) = \frac{1}{6} \cdot 0 = 0$
<br><br>

А теперь найдем вероятность того же события на двух разных костях:

$\displaystyle P(A) = \frac{m}{n} = \frac{1}{6}$

$\displaystyle P(B) = \frac{m}{n} = \frac{1}{6}$

$\displaystyle P(AB) = P(A) \cdot P(B) = \frac{1}{6} \cdot \frac{1}{6} = \frac{1}{36}$

Что нужно делать, если для пар событий нужно определить вероятность наступления только одного из них? Ответ очевиден - складывать:

Для совместных событий:

$\displaystyle P(A \cup B) = P(A) + P(B) = \frac{1}{6} + \frac{1}{6} = \frac{1}{3}$

Для несовместных событий:

$\displaystyle P(A \cup B) = P(A) + P(B) - P(AB) = \frac{1}{6} + \frac{1}{6} - \frac{1}{36} = \frac{11}{36}$

(вычитаем вероятность одновременного наступления, чтобы не увеличивать площадь пересеченных множеств)

### Формула полной вероятности

Если событие А может наступить только при  наступлении событий $B_1, B_2, B_3 \ldots B_n$ образующих полную группу событий (это означает, что при отдельном испытании обязательно произойдет одно из них), то вероятность события А вычисляется по формуле:

$\displaystyle P(A) = P(B_1) \cdot P(A|B_1) + P(B_2) \cdot P(A|B_2) + \ldots + P(B_n) \cdot P(A|B_n)$

---
**Задача 07.** В первой корзине 3 красных мяча и 5 зеленых, во второй - все красные, а в третьей - все зеленые. Случайным образом выбирается корзина и случайным образом из нее берут мяч. Какова вероятность, что мяч окажется зеленым? (для формулы полной вероятности)

Определим вероятность извлечь зеленый мяч из каждой корзины:

$\displaystyle P(A|B_1) = \frac{3}{8}$

$\displaystyle P(A|B_2) = 0$

$\displaystyle P(A|B_3) = 1$

Теперь, исходя из того, что выбор любой из корзин равновероятен:

$\displaystyle P(A) = P(B_1) \cdot P(A|B_1) + P(B_2) \cdot P(A|B_2) + P(B_3) \cdot P(A|B_3) = \frac{1}{3} \cdot \frac{3}{8} + \frac{1}{3} \cdot 0 + \frac{1}{3} \cdot 1 = \frac{13}{24}$

---
### Формула Байеса

Если возникает необходимость определить вероятность события B, если событие A уже произошло, используют формулу Байеса:

$\displaystyle P(B|A) = \frac{P(A|B) \cdot P(B)}{P(A)}$

(здесь *P(B)* - априорная вероятность, которая рассчитывается до испытания, а *P(B|A)* - апостериорная вероятность)

Эту формулу, тоже лучше рассмотреть на задаче (задача 08)

---
**Задача 08.** В первой корзине 3 красных мяча и 5 зеленых, во второй - все красные, а в третьей - все зеленые. Случайным образом выбирается корзина и случайным образом из нее берут зеленый мяч. Какова вероятность, что мяч окажется из третьей корзины? (для формулы Байеса)

$\displaystyle P(B_3|A) = \frac{P(A|B_3) \cdot P(B_3)}{P(A)}$


Вероятность получить зеленый мяч из третьей корзины равна:

$\displaystyle P(A|B_3) = 1$

Выбор корзины равновероятен, значит априорная вероятность выбора третьей корзины равна:

$\displaystyle P(B_3) = \frac{1}{3}$

Ну и полная вероятность вытащить зеленый шар из трез корзин, исходя из решения предыдущей задачи, равна:

$\displaystyle P(A) = \frac{13}{24}$

Соберем формулу:

$\displaystyle P(B_3|A) = \frac{1 \cdot \frac{1}{3}}{\frac{13}{24}} = \frac{24}{39} = \frac{8}{13}$

---
**Задача 09.** Пациент приходит к врачу, чтобы сделать тест на конкретное заболевание. Вероятность положительного теста при том, что болезнь есть 90%. Вероятность отрицательного теста, при том, что человек здоров 95%. Вероятность заболевания 2%. Используя теорему Байеса, найти вероятность, что человек болен, при условии, что тест положительный?

Сначала определимся:

- P(A) - тест положительный
- P(A|B) - тест положительный при условии, что человек болен
- P(B) - вероятность заболевания

Сначала рассчитаем P(A) среди здоровых (*з*) и больных (*б*):

$\displaystyle P(A) = P(A_з|B) \cdot P(B_з) + P(A_б|B) \cdot P(B_б)  = 0.05 \cdot (1 - 0.02) + 0.9 \cdot 0.02 = 0.067$

$\displaystyle P(B|A) = \frac{0.9 * 0.02}{0.067} = 0.2687$


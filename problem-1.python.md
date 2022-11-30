https://projecteuler.net/problem=1 `Multiples of 3 or 5`

> If we list all the natural numbers below 10 that are multiples of 3 or 5, we get 3, 5, 6 and 9. The sum of these multiples is 23.
> 
> Find the sum of all the multiples of 3 or 5 below 1000.

<details>
<summary>Answer:</summary>
233168 
</details>

Od początku. Mamy dane liczby naturalne (czyli całkowite dodatnie bez zera) poniżej 10. 

Wszystkie to 1,2,3,4,5,6,7,8,9. 

Potrzebujemy te co są wielokrotnością 3 i 5. 

Są to 3, 5, 6 i 9.

Na razie rozpatrujemy poniżej 10, wiec 10 jako wielokrotność na razie nie bierzemy pod uwagę.

Skoro mamy znalezione 3, 5, 6 i 9 to ich suma to 23.

Teraz potrzebujemy znaleźć sumę wszystkich wielokrotności 3 i 5 poniżej 1000.

No to jedziemy.

A... będę pisał kod po angielsku, przyzwyczajenie, ale komentarze mogę zrobić po polsku.

Na początku potrzebujemy np. funkcji, która będzie nam sprawdzać czy liczba jest podzielna przez 3.

```python
def multiples(number):
    if number % 3 == 0:
        return True

print(multiples(3))
print(multiples(6))
print(multiples(9))
print(multiples(5))
```

    True
    True
    True
    None

ok, dla 3 działa, ale dla 5 nie
no to zróbmy by działało też dla 5

```python
def multiples(number):
    if number % 3 == 0:
        return True

if number % 5 == 0:
    return True

print(multiples(3))
print(multiples(6))
print(multiples(9))
print(multiples(5))
```

```
True
True
True
True
```

No ale wygląda to mało elegancko... choć po prawdzie wygląda to do dupy. 

Zrobimy refaktor tej funkcji (tak, postaram się też przemycać słownictwo fachowe, żeby się z nim obyć).

```python
def multiples(number):
    if number % 3 == 0 or number % 5 == 0:
        return True

print(multiples(1))
print(multiples(2))
print(multiples(3))
print(multiples(4))
print(multiples(5))
print(multiples(6))
print(multiples(7))
print(multiples(8))
print(multiples(9))
```

```
None
None
True
None
True
True
None
None
True
```
Ok, core problemu już jest ogarnięty. Teraz zrobimy PoC (Proof of Concept).

Wiemy, że poniżej 10, suma to 23.
```python
def multiples(number):
    if number % 3 == 0 or number % 5 == 0:
        return True

sum = 0
for i in range(10):
    if multiples(i):
        sum = sum + i  # lub krócej można zapisać "sum += i"
print(sum)
```
`sum = 0` utworzenie zmiennej (globalnej dla pliku z racji jej pozycji) o nazwie sum z początkową wartością równą zero

`for i in range(10):` to pętla od 0 do 9

`multiples` zwraca `True` dla wielokrotności 3 i 5, a dla pozostałych liczb `None`

no i `print` wypisuje wynik czyli wartość sum na konsolę
```
23
```
wygląda na to, że działa

no to zmieniamy `10` na `1000`

... i mamy wynik, który wkleiłem na samym początku jako **dropdown**

Słowem wyjaśnienie jeszcze wspomnę co robi operator modulo czyli `%`.

Otóż zwraca on resztę z dzielenia przez jakąś liczbę.
```python
In [1]: 1%3
Out[1]: 1

In [2]: 2%3
Out[2]: 2

In [3]: 3%3
Out[3]: 0

In [4]: 4%3
Out[4]: 1

In [5]: 5%3
Out[5]: 2

In [6]: 6%3
Out[6]: 0

In [7]: 7%3
Out[7]: 1

In [8]: 8%3
Out[8]: 2

In [9]: 9%3
Out[9]: 0
```
a tu dla 5
```python
In [10]: 1%5
Out[10]: 1

In [11]: 2%5
Out[11]: 2

In [12]: 3%5
Out[12]: 3

In [13]: 4%5
Out[13]: 4

In [14]: 5%5
Out[14]: 0

In [15]: 6%5
Out[15]: 1

In [16]: 7%5
Out[16]: 2

In [17]: 8%5
Out[17]: 3

In [18]: 9%5
Out[18]: 4

In [19]: 10%5
Out[19]: 0
```

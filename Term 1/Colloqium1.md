# Вопросы
<details><summary>1. Оценка сложности алгоритма по времени </summary>
<center><h1> Оценка сложности по времени </h1></center>
<br><h2> Оценка сложности алгоритма </h2><br>

<h3>

**(a)** **O(g(n))** — *верхняя оценка* сложности алгоритма. Запись **T(n) = O(g(n))** означает, что существуют **C > 0, N > 0** такие, что для любого **n >= N** будет выполняться **0 <= T(n) <= C·g(n)**.

**(b)** **Ω(g(n))** — *нижняя оценка* сложности алгоритма. Запись **T(n) = Ω(g(n))** означает, что существуют **C > 0, N > 0** такие, что для любого **n >= N** будет выполняться **0 <= C·g(n) <= T(n)**. Можно сказать, что **T(n) = Ω(g(n))**, если **g(n) = O(T(n))**.

**(c)** **θ(g(n))** — *точная оценка* сложности алгоритма. Запись **T(n) = θ(g(n))** означает, что существуют **C, K > 0, N > 0** такие, что для любого **n >= N** будет выполняться **0 <= C·g(n) <= T(n) <= K·g(n)**. *Точная оценка* сложности алгоритма будет существовать в том случае, если *верхняя* и *нижняя оценка* будут равны.

</h3>
<img src = "source/AlgorithmAnalysis.png">

<br><h2> Свойства О </h2><br>

<h3>

**T1(n) = O(g1(n))**, **T2(n) = O(g2(n))**

1. *Сложность суммы*: **T1 + T2 = O(max(g1(n), g2(n)))**.

2. *Сложность произведения*: **T1·T2 = O(g1(n)·g2(n))**.

3. *Умножение на константу*: **C·T1 = O(g1(n))**.

4. *Сумма с константой*: **C + T1 = O(g1(n))**.

5. *Теорема о связи* **O**, **Ω**, **θ**: **T(n) = θ(g(n)) <=> T(n) = O(g(n))** и **T(n) = Ω(g(n))**.

</h3>

<br><h2> Классификация алгоритмов </h2><br>

<h3>

Можно выделить следующие типы временной сложности:

1. *Постоянный*: **O(1)**

2. *Логарифмический*: **O(log(n))**

3. *Линейный*: **O(n)**.

4. *Квадратичный*: **O(n^2)**.

5. *Кубический*: **O(n^3)**.

6. *Полиноминальный*: **O(n^m)**.

7. *Экспоненциальный* **O(t^p(n))**, **t** — константа, **p(n)** — некоторая полиноминальная функция.

8. *Факториальный*: **O(n!)**. Обладает наибольшей временной сложностью среди всех известных типов.

</h3>

<img src = "source/AlgorithmClassification.png">

</details>
<details><summary>2. Оценка сложности алгоритма по памяти</summary>
То же самое, что и по времени только по памяти...
</details>
<details><summary>3. Сортировка вставками</summary>
  <center><h1> Сортировка вставками </h1></center>
  <br><h2> Асимптотика алгоритма </h2><br>
 
<h3>

| Оценка     | Лучший случай | Средний случай | Худший случай |
|:----------:|:-------------:|:--------------:|:-------------:|
| По времени | O(n)          | O(n^2)         | O(n^2)        |
| По памяти  | O(1)          | O(1)           | O(1)          |

  <br><h2> Устойчивость </h2><br>

  <p><h3><strong>Сортировка вставками</strong> является устойчивой.</h3></p>

</h3>


  Лучший случай достигается, при изначально отсортрованном массиве.
  Инвариант цикла — логическое выражение, истинность которого сохраняется после каждого прохода тела цикла.
  Инвариант: на j-й итерации цикла массив [0..(j-1)] состоит из исходных элементов, расположенных в порядке возрастания.

  На первой итерации алгоритм состоит из 1 исходного элемента, расположенного по возрастанию.

  <h3>    
  <img src = "source/InsertionSort.gif">

  <br><center><h1> Реализация </h1></center><br>

```c++
bool CmpToIntLower(int &a, int &b) {
  return a < b;
}


template<class T, class Compare>
void InsertionSort(vector<T> &a, Compare cmp = CmpToIntLower) {
    for (int i = 1; i < a.size(); ++i) {
        int j = i-1;
        while  (j >= 0 && CmpToIntLower(a[j + 1], a[j])){
            swap(a[j+1],a[j]);
            j--;
        }
    }
}
```

</details>
<details><summary>4. Сортировка слиянием</summary>
  <center><h1> Сортировка Слиянием </h1></center>
  <br><h2> Асимптотика алгоритма </h2><br>

  <h3>

| Оценка     | Лучший случай | Средний случай | Худший случай |
|:----------:|:-------------:|:--------------:|:-------------:|
| По времени | O(n * log(n)) | O(n * log(n))  | O(n * log(n)) |
| По памяти  | O(n)          | O(n)           | O(n)          |

  <p><h3>*Сортировка слиянием* является устойчивой.</h3></p>

  <br>По времени: n тратится на слияние, log(n) на разбиение через вызов рекурсии. 

  !Необходим дополнительный массив при слиянии.
  </h3>    
  <img src = "source/MergeSort.png">
  <br><center><h1> Реализация </h1></center><br>
  <h2> Рекурсивное разбиение исходного массива </h2>

```c++
template<class T, class Compare>
void MergeSortRecursive(vector<T>& a, int left, int right, Compare& cmp = CmpToIntLower) {
    if (right - left <= 1) {
        return;
    }
    if (right - left == 2) {
        if (cmp(a[left], a[left + 1])) swap(a[left], a[left + 1]);
    }
    int mid = left + (right - left) / 2;
    MergeSortRecursive(a, left, mid, cmp);
    MergeSortRecursive(a, mid, right, cmp);
    //merge(a.begin()+left,a.begin()+mid,a.begin()+mid,a.begin()+right, back_inserter(tmp));
    vector<T> tmp = my_merge(a, left, mid, mid, right, cmp);
    copy(tmp.begin(), tmp.end(), a.begin() + left);
} 
```

<br><h2>Нерекурсивное разбиение исходного массива</h2>

```c++
template<class T, class Compare>
void MergeSortNotRecursive(vector<T>& a, Compare cmp = CmpToIntLower) {
    int step = 1;
    while (step < a.size()) {
        int i = 0;
        vector<T> b;
        while (i * 2 * step <= a.size()) {
            int l1 = i * 2 * step, r1 = l1 + step, l2 = l1 + step, r2 = min(l2 + step, (int) a.size());
            if (l2 < a.size()) {
                //merge(a.begin()+l1,a.begin()+r1,a.begin()+l2,a.begin()+r2, back_inserter(b));
                vector<T> tmp = my_merge(a, l1, r1, l2, r2, cmp);
                copy(tmp.begin(), tmp.end(), back_inserter(b));
            } else {
                r1 = min(l1 + step, (int) a.size());
                copy(a.begin() + l1, a.begin() + r1, back_inserter(b));
            }
            i++;
        }
        a = b;
        step += step;
    }
}
```
<br><h2> Слияние разбитых массивов </h2>

```c++
bool CmpToIntLower(int& a, int& b) {
    return a < b;
}


template<class T, class Compare>
vector<T> my_merge(vector<T>& a, int l1, int r1, int l2, int r2, Compare cmp) {
    vector<T> temp;
    while (l1 < r1 && l2 < r2) {
        if (cmp(a[l1], a[l2])) {
            temp.push_back(a[l1++]);
        } else {
            temp.push_back(a[l2++]);
        }
    }
    while (l1 < r1) temp.push_back(a[l1++]);
    while (l2 < r2) temp.push_back(a[l2++]);
    return temp;
}
```


</details>
<details><summary>5. Быстрая сортировка</summary>

  <center><h1> Быстрая сортировка </h1></center>
  <br><h2> Асимптотика алгоритма </h2><br>
 
<h3>

| Оценка     | Лучший случай | Средний случай | Худший случай |
|:----------:|:-------------:|:--------------:|:-------------:|
| По времени | O(n·log(n))   | O(n·log(n))    | O(n^2)        |
| По памяти  | O(log(n))     | O(log(n))      | O(n)          |

*Худший случай* — когда на каждом разбиении массив делится на одноэлементный массив и массив длины **n - 1**.

**log(n)** в оценке памяти — глубина рекурсии.
</h3>

<h2> Разбиение Ломуто </h2>

<h3>

*Опорный элемент* — последний элемент массива.

</h3>

<br><center><h1> Реализация </h1></center><br>

```c++
int partitionLomuto(vector<T> &a,int l, int r, Compare &cmp) {
    T pivot = a[r];
    int i = l - 1;
    for (int j = l; j < r; ++j) {
        if (cmp(a[j], pivot)){  //cmp: <= >=
            i++;
            swap(a[i],a[j]);
        }
    }
    swap(a[i+1],a[r]);
    return i + 1;
}

void QuickSortL(vector<T> &a,int l, int r, Compare &cmp){
    if (l < r){
        int p = partitionLomuto(a,l,r,cmp);
        QuickSortL(a,l,p - 1,cmp);
        QuickSortL(a,p + 1,r,cmp);
    }
}
```
<img src = "source/QuickSort.png">

<h2> Разбиение Хоара </h2>

<h3>

*Опорный элемент* — элемент посередине массива.

*Разбиение Хоара* эффективнее Ломуто, так как происходит в среднем в **3** раза меньше свапов, и разбиение эффективнее, когда все элементы равны.

</h3>

  <br><center><h1> Реализация </h1></center><br>

```c++
void QuickSortH(vector<T> &a,int l, int r, Compare &cmp){
    int i,j;
    T k = a[l + (r-l)/2];
    i = l;
    j = r;
    do {
        while (cmp(a[i],k)) i++;  // cmp: > <
        while (cmp(k,a[j])) j--;
        if (i<=j){
            swap(a[i],a[j]);
            i++;
            j--;
        }
    } while (i < j);
    if (l < j) QuickSortH(a,l,j,cmp);
    if (i < r) QuickSortH(a,i,r,cmp);
}
```

<h2> Модификации </h2>

<h3>

1.  Выбор *опорного элемента* случайным образом.

2.  Выбор *опорного элемента*, как среднее между крайным левым и крайним правым значением массива.

</h3>

<h2> Устойчивость </h2>

<h3>

*Быстрая сортировка* не является устойчивой сортировкой из-за свапов при разбиении на два массива.

</h3>



</details>
<details><summary>6. Сортировка подсчетом</summary>

  <center><h1> Сортировка подсчетом (первая вариация) </h1></center>
  <br><h2> Асимптотика алгоритма </h2><br>
 
<h3>

| Оценка     | Лучший случай | Средний случай | Худший случай |
|:----------:|:-------------:|:--------------:|:-------------:|
| По времени | O(k + n)      | O(k + n)       | O(k + n)      |
| По памяти  | O(k)          | O(k)           | O(k)          |

В данной реализации исходный массив **A[n]** состоит из целых чисел от **0** до **k - 1**. Массив **C[k]** для подсчета количества повторений каждого числа в массиве **A**. После этого в **A** последовательно каждый **i** записывается **C[i]** раз.

</h3>

<h2> Устойчивость </h2>

<h3>

Данная реализация сортировки подсчетом не является устойчивой, так как идет перезапись каждого элемента.

</h3>

<img src = "source/CountingSort1.gif">

  <br><center><h1> Реализация </h1></center><br>

```c++
void SimpleCountingSort(vector<int>& a) {
    int maxn = 0;
    for (int i = 0; i < a.size(); ++i) {
        maxn = max(maxn, a[i]);
    }
    maxn++;
    vector<int> cnt(maxn, 0);
    for (auto el: a) {
        cnt[el]++;
    }
    a.clear();
    a.resize(0);
    for (int number = 0; number < maxn; ++number) {
        for (int j = 0; j < cnt[number]; ++j) {
            a.push_back(number);
        }
    }
}
```

  <center><h1> Сортировка подсчетом (вторая вариация) </h1></center>
  <br><h2> Асимптотика алгоритма </h2><br>
 
  <h3>

| Оценка     | Лучший случай | Средний случай | Худший случай |
|:----------:|:-------------:|:--------------:|:-------------:|
| По времени | O(k + n)      | O(k + n)       | O(k + n)      |
| По памяти  | O(k + n)      | O(k + n)       | O(k + n)      |

В данной реализации мы начинаем сортировку аналогично первой вариации. Исходный массив **A[n]** состоит из целых чисел от **0** до **k - 1**. Массив **C[k]** для подсчета количества повторений каждого числа в массиве **A**. После того, как мы посчитали количество каждого **i**, мы определяем индекс последнего элемента **i** в отсортированном массиве. Создаем вспомогательный массив **B[n]** и в него, идя по **A** с конца, записываем каждый **i** по индексу из **C**. Индекс записанного только что элемента уменьшаем на **1**. (думаю на коде станет понятнее).

</h3>

<h2> Устойчивость </h2>

<h3>

Данная реализация сортировки подсчетом является устойчивой. Мы расставляем объекты с одинаковыми значениями ключа сортировки по их исходным позициям относительно друг друга.

</h3>

<h2> Модификации </h2>

<h3>

1. С помощью линейного поиска *максимума* и *минимума* находим диапазон чисел. Это не влияет на асимптотику алгоритма, так как поиск выполняется за **O(n)**.

2. *Минимум* может быть отрицательным, в то время как в **C** индексы от **0** до **k - 1**. Поэтому при работе с массивом **C** нужно вычитать *минимум* из **A[i]**, а при записи в **B[i]** прибавлять его.

</h3>

<h3> 

Единственное, что в графической реализации мы идем с начала массива **A**, это делает сортировку неустойчивой. Если мы будем идти с конца (т.е. как и описывалось), то сортировка станет устойчивой.

</h3>

<img src = "source/CountingSort2.gif">

  <br><center><h1> Реализация </h1></center><br>

```c++
void CountingSort(vector<int>& a) {
    int maxn = 0;
    for (int i = 0; i < a.size(); ++i) {
        maxn = max(maxn, a[i]);
    }
    maxn++;
    vector<int> cnt(maxn, 0);
    for (auto el: a) {
        cnt[el]++;
    }
    for (int number = 1; number < maxn; ++number) {
        cnt[number] += cnt[number-1];
    }
    vector<int> carry(a.size(),0);

    for (int i = a.size() - 1; i >= 0; --i) {
        carry[--cnt[a[i]]] = a[i];
    }
    a = carry;
}  
```


</details>
<details><summary>7. Цифровая сортировка</summary>

  <center><h1> Цифровая сортировка </h1></center>

  <br><h2> Асимптотика алгоритма </h2><br>
 
<h3>

| Оценка     | Лучший случай | Средний случай | Худший случай |
|:----------:|:-------------:|:--------------:|:-------------:|
| По времени | O(m·T(n))     | O(m·T(n))      | O(m·T(n))     |
| По памяти  | O(M(n))       | O(M(n))        | O(M(n))       |

**T(n)** и **M(n)** — сложности по времени и памяти сортировки, которая используется для разрядов. В конкретно этой реализации, мы используем устойчивую сортировку подсчетом. **m** — количество разрядов сортируемых элементов.

| Оценка     | Лучший случай | Средний случай | Худший случай |
|:----------:|:-------------:|:--------------:|:-------------:|
| По времени | O(m·n)        | O(m·n)         | O(m·n)        |
| По памяти  | O(k + n)      | O(k + n)       | O(k + n)      |

Алгоритм представляет собой цикл по номеру разряда, начиная с правого (младшего). На каждой итерации элементы массива **A** размещаются в нужном порядке во вспомогательном массиве **B**. Причём кол-во возможных элементов в A равно k. Для сортировки на каждой итерации цикла по разрядам используется *устойчивая сортировка подсчетом*.

Конкретная реализация *цифровой сортировки* называется *LSD-сортировкой* — цикл идет по разрядам, начиная с младшего, то есть справа.

Существует модификация, в которой мы начинаем со старшего разряда (слева). Она называется *MSD-сортировкой*.
</h3>

<img src = "source/RadixSort.png">

  <br><center><h1> Реализация </h1></center><br>

```c++
void radixSortInt(vector<int> &a, int m){
    for (int dig = 0; dig < m; ++dig) {
        int k = 10;
        vector<int> cnt(k, 0);
        for (auto el: a) {
            cnt[get_digit(el,dig)]++;
        }
        int count = 0;
        for (int number = 0; number < k; ++number) {
            int tmp = cnt[number];
            cnt[number] = count;
            count += tmp;
        }
        vector<int> carry(a.size(),0);

        for (int i = 0; i < a.size(); ++i) {
            int d = get_digit(a[i], dig);
            carry[cnt[d]++] = a[i];
        }
        a = carry;
    }
}  
```

<h3>

Релизация для строк. Сложность по памяти будет **O(n)**, сложность по времени не изменится.

</h3>

  <br><center><h1> Реализация </h1></center><br>

```c++
void radixSortStrings(vector<string> &a, int m){ //make sure size of all strings = m
    for (int digit = m - 1; digit >= 0; digit--) {
        vector<string> temp_arr;
        for (int letter = 0; letter <= 26; letter++) { //26 = 'z' - 'a' + 1
            for (string& item: a) {
                if (item[digit] == char(letter + 'a')) temp_arr.push_back(item);
            }
        }
        a = temp_arr;
    }
}
```

</details>
<details><summary>8. Стек</summary>
  <center><h1> Стек </h1></center>
  <br><center><h2> Оценка операций структуры по времени </h2></center><br>
  <h3>

| Удаление | Добавление | Поиск |
|:--------:|:----------:|:-----:|
|   O(1)   |    O(1)    |  O(n) |


  <h2><center> Описание структуры </center><h2>
  <h3>
  <p>Stack - абстрактный тип данных, представляющий собой список элементов, организованных по принципу LIFO (англ. last in — first out, «последним пришёл — первым вышел»). </p>

  <p>Если проще, то Stack можно представить в виде стопки книг (для того, чтобы добраться до определенной книги необходимо убрать сверху все остальные). </p> 

  <p>Стек состоит из ячеек(в примере — это книги), которые представлены в виде структуры, содержащей какие-либо данные и указатель типа данной структуры на следующий элемент.</p>
  </h3>
  <h3><br>   
  <img src = "source/Stack.gif">

   <h2>Stack поддерживает следующие операции: </h2>
<h3>

* Добавление элемента в начало
* Удаление верхнего элемента
* Проверка на наличие элементов
* Обращение к первому элементу
</h3>

<br><h2>Добавление в начало</h2><br>
<h3>
<p>Для добаления нового элемента в Stack мы создаем ячейку с необходимым нам значением.
<strong>

* Если Stack оказывается пустым, то мы делаем ячейку head.
* Если в Stack хранится какой-либо элемент, то мы ставим указатель нового элемента на head и только потом делаем данную ячейку head.  
</strong>
</h3>

```c++
void push(T val){
    Node<T>* elem = new Node<T>;
    elem->value = val;
    if (top != nullptr){
        elem->prev = top;
        top = elem;
    } else {
        top = elem;
    }
}
```

<br><h2>Удаление элемента</h2><br>

<h3>
<p>Для удаления элемента в Stack мы сохраняем адрес головы, переназначаем первый элемент (делаем второй первым), <strong>чистим за собой память</strong> и только потом удаляем элемент.
</h3>

```c++
void pop(){
    Node<T>* to_del = top;
    top = top->prev;
    delete to_del;
}
```

<br><h2> Проверка на наличие элементов </h2><br>

```c++
bool empty(){
    return (top == nullptr);
}
```

<br><h2> Обращение к первому элементу </h2><br>

```c++
T back(){
    T ans = top->value;
    return ans;
}
```
<br><h2> Полная реализация </h2><br>

```c++
template<class T>
struct Stack{
    Node<T>* top;
    Stack(){
        top = nullptr;
    }
    void push(T val){
        Node<T>* elem = new Node<T>;
        elem->value = val;
        if (top != nullptr){
            elem->prev = top;
            top = elem;
        } else {
            top = elem;
        }
    }

    void pop(){
        Node<T>* to_del = top;
        top = top->prev;
        delete to_del;
    }

    T back(){
        T ans = top->value;
        return ans;
    }

    bool empty(){
        return (top == nullptr);
    }
};
```

  
</details>
<details><summary>9. Очередь </summary>
<h2><center>Очередь</center></h2><br>

<h3>

| Удаление | Добавление | Поиск |
|:--------:|:----------:|:-----:|
|   O(1)   |    O(1)    |  O(n) |

</h3>

<h2> Описание структуры <br></h2>

<h3>

<p>Queue — абстрактный тип данных, представляющий собой список элементов, организованных по принципу FIFO (англ. first in — first out, «первым пришёл — первым вышел»).</p>

* head - голова очереди (отсюда удаляются элементы).
* tail - хвост очереди (сюда добавляются элементы).

<br> Очередь поддерживает следующие операции: <br>

* push - операция вставки элемента (в конец).
* pop - операция удаление элемента (из начала). 
* size - операция получения количества элементов в очереди.
* empty - проверка очереди на наличие в ней элементов.
* top - возвращает элемент из начала.
</h3>

<img src = "source/Queue.png">

<br><h2>Добавление элемента в конец</h2><br>
<h3><p>Добавление элемента в конец осуществляется по следующему принципу:
</p>

1. Создается новая ячейка, указывающая на nullptr и имеющая необходимое нам значение. 
2. Проверяется: есть ли элементы в очереди.
3. *(1)* <strong> Если элементов нет</strong>, то первый и последний элементы становятся равны новой ячейке. 
3. *(2)* <strong> Если элементы есть</strong>, то мы делаем так, чтобы последний элемент стал указывать на новый, и чтобы последний tail был равен новому элементу. 
</h3>

```c++
void push(T val){
    Node<T>* elem = new Node<T>;
    if (last != nullptr){
        last->next = elem;
    } else {
        first = elem;
    }
    elem->value  = val;
    elem->next = nullptr;
    last = elem;
}
```

<br><h2>Удаление элемента</h2><br>
<h3><p> Удаление элемента осуществляется по следующему принципу:</p>

1. Создается ячейка для удаления, равная tail.
2. head становиться вторая ячейка.
3. Если после удаления очередь стала пустой, то присваиваем tail nullptr.
4. Чистим память, на которую указывает ячейка.
5. Удаляем ячейку.

</h3>



```c++
void pop(){
    Node<T>* to_del = first;
    first = first->next;
    if (first == nullptr)
    {
        last = nullptr;
    }
    delete to_del;
}
```

<br><h2>Вывод первого элемента</h2><br>

```c++
T front(){
    T ans = first->value;
    return ans;
}
```

<br><h2>Полная реализация</h2><br>

```c++
template<class T>
struct Node {
    T value;
    Node *next;
};

template<class T>
struct Queue{
    Node<T>* first;
    Node<T>* last;
    Queue(){
        first = nullptr;
        last = nullptr;
    }
    void push(T val){
        Node<T>* elem = new Node<T>;
        if (last != nullptr){
            last->next = elem;
        } else {
            first = elem;
        }
        elem->value  = val;
        elem->next = nullptr;
        last = elem;
    }

    void pop(){
        Node<T>* to_del = first;
        first = first->next;
        if (first == nullptr)
        {
            last = nullptr;
        }
        delete to_del;
    }

    T front(){
        T ans = first->value;
        return ans;
    }
};  
```
<br><h2>Очередь на стеках</h2><br>

Главное условие, которое должно быть выполнено — все операции должны выполняться за амортизированное O(1).

Возьмем два стека: s1 и s2.

Операцию push будем всегда делать в стек s1.

Операция pop будет устроена так: если стек s2 пустой, перекладываем все элементы из s1 в s2 последовательными вызовами pop и push. Теперь в стеке s2 лежат элементы в обратном порядке (самый верхний элемент — это самый первый положенный элемент в нашу очередь).

Если s2 не пуст, тупо достаем элементы из него. Как только s2 окажется снова пустым повторяем ту же операцию.
</details>
<details><summary>10. Односвязный список</summary>
<center><h1> Односвязный список </h1></center>
<img src = "source/List1.png">
<br><h2>Добавление элемента в начало</h2><br>
<img src = "source/addNewEl.png">   
<h2> Пояснение: </h2>
<h3><p> Для того, чтобы добавить новую Node в начало мы переприсваиваем указатель head на новую Node и делаем новый элемент head.</p></h3>
<br><h2> Добавление элемента в середину </h2><br>
<img src = "source/addNewNode.png">
<h2> Пояснение: </h2>
<h3><p> Для того, чтобы добавить новую Node в середину необходимо: переопределить указатель новой Node на следующий элемент, а указатель предыдущего элемента - на новую. </p></h3>
<br><h2> Удаление Node </h2><br>
<img src = "source/delNode.png">
<h2> Пояснение: </h2>
<h3><p> Мы переназначиваем указатель предыдущего Node на следующую после того Node, которую хотим удалить. Зануляем указатель <strong>и не забываем почистить за собой память(т.е. сделать delete) </strong></p></h3>

<br><center><h1> Реализация </h1></center><br>

```c++
template <class T>

struct Node {
	T value;
	Node* next = nullptr;
};

template <class T>
struct LinkedList {
	Node<T>* first;
	Node<T>* last;
	LinkedList() {
		first = nullptr;
		last = nullptr;
	}
	void Push(T val) {
		Node<T>* new_node = new Node<T>;
		new_node->value = val;
		if (last == nullptr) {
			last = new_node;
			first = new_node;
			return;
		}
		last->next = new_node;
		last = new_node;
	}
	void PopFirst() { // deleting first
		if (first->next == nullptr) {
			last = nullptr;
			first = nullptr;
			return;
		}
		first = first->next;
	}
	void PopLast() { // deleting last
		if (first->next == nullptr) {
			last = nullptr;
			first = nullptr;
			return;
		}
		Node<T>* point = first;
		while (point->next != last) {
			point = point->next;
		}
		last = point;
		last->next = nullptr;
	}
	void Insert(T val, uint64_t pos) { // pos = number of postinions after first
		if (last == nullptr) {
			Push(val);
			return;
		}
		Node<T>* new_node = new Node<T>;
		new_node->value = val;
		if (pos == 0) {
			new_node->next = first;
			first = new_node;
			return;

		}
		Node<T>* point = first;
		while (pos > 1) {
			pos--;
			point = point->next;
		}

		if (point == last) {
			Push(val);
			return;
		}

		new_node->next = point->next;
		point->next = new_node;
	}
	void Delete(uint64_t pos) { // pos = number of postinions after first
		if (pos == 0) {
			PopFirst();
			return;
		}
		Node<T>* point = first;
		while (pos > 1) {
			pos--;
			point = point->next;
		}
		if (point->next == last) {
			PopLast();
			return;
		}
		point->next = point->next->next;
	}
	T Front() {
		return first->value;
	}
	T Back() {
		return last->value;
	}
	T Get(uint64_t pos) {
		if (pos == 0) {
			return Front();
		}
		Node<T>* point = first;
		while (pos) {
			pos--;
			point = point->next;
		}
		return point->value;
	}
	T GetMax() {
		T maxel = first->value;
		Node<T>* point = first->next;
		while (point != first) {
			maxel = max(maxel, point->value);
			point = point->next;
		}
		return maxel;
	}
	T GetMin() {
		T minel = first->value;
		Node<T>* point = first->next;
		while (point != first) {
			minel = min(minel, point->value);
			point = point->next;
		}
		return minel;
	}
};
```
</details>

<details><summary>11. Двусвязный список</summary>
<center><h1> Двусвязный список </h1></center>
<img src = "source/List2.png">
<br><h2>Добавление элемента в начало</h2><br>
<img src = "source/addNewNode2Head.png">
<h2>Пояснение:<h2>
<h3>

1. Создаем новую Node.
2. Ставим указатель prev новой Node на head.
3. Ставим указатель next head на Node.
4. переопрделяем head на новую Node.
</h3>


<br><h2>Добавление элемента в определенное место</h2><br>
<img src = "source/addNewNode2_.png">
<h2>Пояснение:<h2>
<h3>

1. Создаем новую Node.
2. Ставим указатель next новой Node на нужное нам место.
3. Ставим указатель prev новой Node на Node.next.prev.
4. Переопределяем prev указатель Node.next на Node.
5. Переопределяем next указатель Node.prev на Node. 
</h3>

<br><h3><p>Удаление Node</p></h3><br>
<img src = "source/delNode2.png">
<h2>Пояснение:</h2>
<h3>

1. Переопределяем указатель Node.prev.next на Node.next.
2. Переопределяем указатель Node.next.prev на Node.prev.
3. Убераем указатели.
4. Удаляем Node.

</h3>


<br><center><h1> Реализация </h1></center><br>

```c++
template <class T>
struct Node {
	T value;
	Node* next = nullptr;
	Node* prev = nullptr;
};

template <class T>
struct LinkedList {
	Node<T>* first;
	Node<T>* last;
	LinkedList() {
		first = nullptr;
		last = nullptr;
	}
	void Push(T val) {
		Node<T>* new_node = new Node<T>;
		new_node->value = val;
		if (last == nullptr) {
			last = new_node;
			first = new_node;
			return;
		}
		new_node->prev = last;
		last->next = new_node;
		last = new_node;
	}
	void PopFirst() { // deleting first
		if (first->next == nullptr) {
			last = nullptr;
			first = nullptr;
			return;
		}
		first = first->next;
		first->prev = nullptr;
	}
	void PopLast() { // deleting last
		if (last->prev == nullptr) {
			last = nullptr;
			first = nullptr;
			return;
		}
		last = last->prev;
		last->next = nullptr;
	}
	void Insert(T val, uint64_t pos) { // pos = number of postinions after first
		if (last == nullptr) {
			Push(val);
			return;
		}
		Node<T>* new_node = new Node<T>;
		new_node->value = val;
		if (pos == 0) {
			new_node->next = first;
			first->prev = new_node;
			first = new_node;
			return;

		}
		Node<T>* point = first;
		while (pos > 1) {
			pos--;
			point = point->next;
		}

		if (point == last) {
			Push(val);
			return;
		}

		new_node->next = point->next;
		new_node->prev = point;
		point->next->prev = new_node;
		point->next = new_node;
	}
	void Delete(uint64_t pos) { // pos = number of postinions after first
		if (pos == 0) {
			PopFirst();
			return;
		}
		Node<T>* point = first;
		while (pos > 1) {
			pos--;
			point = point->next;
		}
		if (point->next == last) {
			PopLast();
			return;
		}
		point->next->next->prev = point;
		point->next = point->next->next;
	}
	T Front() {
		return first->value;
	}
	T Back() {
		return last->value;
	}
	T Get(uint64_t pos) {
		if (pos == 0) {
			return Front();
		}
		Node<T>* point = first;
		while (pos) {
			pos--;
			point = point->next;
		}
		return point->value;
	}
	T GetMax() {
		T maxel = first->value;
		Node<T>* point = first->next;
		while (point != first) {
			maxel = max(maxel, point->value);
			point = point->next;
		}
		return maxel;
	}
	T GetMin() {
		T minel = first->value;
		Node<T>* point = first->next;
		while (point != first) {
			minel = min(minel, point->value);
			point = point->next;
		}
		return minel;
	}
};
```

</details>
<details><summary>12. Циклический список</summary>

<center><h1> Циклический список </h1></center>

<h3>

*Циклическиий список* - это односвязный список, первый элемент которого является следующим для последнего.

</h3>

<img src = "source/CycledList1.png">


<h3>

|Добавление в начало|Добавление в конец|Добавление в определенное место|
|:-----------------:|:----------------:|:-----------------------------:|
|O(1)               |O(1)              |O(n)                           |

|Удаление из начала|Удаление из конца|Удаление по индексу|
|:----------------:|:---------------:|:-----------------:|
|O(1)              |O(n)             |O(n)               |


</h3>

<br><center><h1> Реализация </h1></center><br>

```c++
template <class T>
struct Node {
	T value;
	Node* next;
};

template <class T>
struct CycleLinkedList {
	Node<T>* first;
	Node<T>* last;
	CycleLinkedList() {
		first = nullptr;
		last = nullptr;
	}
	void Push(T val) {
		Node<T>* new_node = new Node<T>;
		new_node->value = val;
		if (last == nullptr) {
			last = new_node;
			first = new_node;
			last->next = new_node;
			first->next = new_node;
			return;
		}
		new_node->next = first;
		last->next = new_node;
		last = new_node;
	}
	void PopFirst() { // deleting first
		if (first->next == first) {
			first = nullptr;
			last = nullptr;
			return;
		}
		last->next = first->next;
		first = first->next;
	}
	void PopLast() { // deleting last
		if (first->next == first) {
			first = nullptr;
			last = nullptr;
			return;
		}
		Node<T>* point = first;
		while (point->next != last) {
			point = point->next;
		}
		point->next = first;
		last = point;
	}
	void Insert(T val, uint64_t pos) { // pos = number of postinions after first
		if (first == nullptr || first->next == first || pos == 0) {
			Push(val);
			return;
		}

		Node<T>* point = first;
		while (pos > 1) {
			pos--;
			point = point->next;
		}

		if (point == last) {
			Push(val);
			return;
		}

		Node<T>* new_node = new Node<T>;
		new_node->value = val;
		new_node->next = point->next;
		point->next = new_node;
	}
	void Delete(uint64_t pos) { // pos = number of postinions after first
		if (pos == 0) {
			PopFirst();
			return;
		}
		Node<T>* point = first;
		while (pos > 1) {
			pos--;
			point = point->next;
		}
		if (point->next == first) {
			PopFirst();
			return;
		}
		else if (point->next == last) {
			PopLast();
			return;
		}

		point->next = point->next->next;
	}
	T Front() {
		return first->value;
	}
	T Back() {
		return last->value;
	}
	T Get(uint64_t pos) {
		if (pos == 0) {
			return Front();
		}
		Node<T>* point = first;
		while (pos) {
			pos--;
			point = point->next;
		}
		return point->value;
	}
	T GetMax() {
		T maxel = first->value;
		Node<T>* point = first->next;
		while (point != first) {
			maxel = max(maxel, point->value);
			point = point->next;
		}
		return maxel;
	}
	T GetMin() {
		T minel = first->value;
		Node<T>* point = first->next;
		while (point != first) {
			minel = min(minel, point->value);
			point = point->next;
		}
		return minel;
	}
};
```

</details>
<details><summary>13. Стек на списках</summary>

  <br><center><h1> Реализация </h1></center><br>

```c++
template<class T>
struct Stack{
    Node<T>* top;
    Stack(){
        top = nullptr;
    }
    void push(T val){
        Node<T>* elem = new Node<T>;
        elem->value = val;
        if (top != nullptr){
            elem->prev = top;
            top = elem;
        } else {
            top = elem;
        }
    }

    void pop(){
        Node<T>* to_del = top;
        top = top->prev;
        delete to_del;
    }

    T back(){
        T ans = top->value;
        return ans;
    }

    bool empty(){
        return (top == nullptr);
    }
};
```

</details>
<details><summary>14. Очередь на списках</summary>

  <br><center><h1> Реализация </h1></center><br>

```c++
  template<class T>
struct Node {
    T value;
    Node *next;
};

template<class T>
struct Queue{
    Node<T>* first;
    Node<T>* last;
    Queue(){
        first = nullptr;
        last = nullptr;
    }
    void push(T val){
        Node<T>* elem = new Node<T>;
        if (last != nullptr){
            last->next = elem;
        } else {
            first = elem;
        }
        elem->value  = val;
        elem->next = nullptr;
        last = elem;
    }

    void pop(){
        Node<T>* to_del = first;
        first = first->next;
        if (first == nullptr)
        {
            last = nullptr;
        }
        delete to_del;
    }

    T front(){
        T ans = first->value;
        return ans;
    }
};  
```
</details>

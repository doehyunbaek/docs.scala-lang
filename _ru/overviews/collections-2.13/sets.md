---
layout: multipage-overview
title: Множества
partof: collections-213
overview-name: Collections
num: 6
previous-page: seqs
next-page: maps
language: ru
---

Множества (`Set`) - это итерируемые сущности, которые не содержат дублирующих друг друга элементов. Операции с множествами описаны в таблицах ниже. Описания включают операции для базовых, неизменяемых и изменяемых множеств. Все их операции поделены на следующие категории:

* **Проверки** `contains`, `apply`, `subsetOf`. Метод `contains` спрашивает, содержит ли множество данный элемент. Метод `apply` для множества работает также как и `contains`, поэтому `set(elem)` является тем же самым, что и `set contains elem`. Это означает, что множества могут использоваться в качестве тестовых функций, которые возвращают `true` при проверке элементов, которые они содержат.

Например:


    scala> val fruit = Set("apple", "orange", "peach", "banana")
    fruit: scala.collection.immutable.Set[java.lang.String] = Set(apple, orange, peach, banana)
    scala> fruit("peach")
    res0: Boolean = true
    scala> fruit("potato")
    res1: Boolean = false


* **Сложения** `incl` и `concat` (либо `+` и `++`, соответственно), которые добавляют один или несколько элементов во множество, создавая новое множество.
* **Удаления** `excl` и `removedAll` (либо `-` и `--`, соответственно), которые удаляют один или несколько элементов из множества, образуя новое множество.
* **Операции с множествами** для объединения, пересечения и установления расхождений во множествах. Каждая из таких операций имеет две формы: словарную и символьную. Словарные версии - `intersect`, `union`, и `diff`, а символьные - `&`, `|` и `&~`. Фактически `++`, которые `Set` унаследовали от `Iterable`, можно рассматривать как еще один псевдоним `union` или `|`, за исключением того, что `++` принимает `IterableOnce` в качестве аргумента, а `union` и `|` принимают множества.
                             
### Операции на Классе Set ###

| ПРИМЕР  	  	    | ЧТО ДЕЛАЕТ				     |
| ------       	       	    | ------					     |
|  **Проверки:**               |						     |
|  `xs contains x`  	    |Проверяет, является ли `x` элементом `xs`.  |
|  `xs(x)`        	    |Тоже самое что и `xs contains x`.                        |
|  `xs subsetOf ys`  	    |Проверяет, является ли `xs` подмножеством `ys`.         |
|  **Добавления:**           |						     |
|  `xs concat ys`<br>или `xs ++ ys`  	            |Множество, содержащее все элементы `xs`, а также все элементы `ys`. |
|  **Удаления:**               |						     |
|  `xs.empty`  	            |Пустое множество того же класса, что и `xs`.         |
|  **Двуместные Операции:**   |						     |
|  `xs intersect ys`<br>или `xs & ys`  	            |Множество содержащее пересечение `xs` и `ys`.          |
|  `xs union ys`<br>или <code>xs &#124; ys</code>  	            |Множество содержащее объединение `xs` и `ys`.                 |
|  `xs diff ys`<br>или `xs &~ ys`  	            |Множество содержащее расхождение между `xs` и `ys`.            |

В неизменяемых множествах методы добавления или удаления элементов работают путем возврата новых множеств (`Set`), как описано ниже.

### Операции на Классе immutable.Set ###

| ПРИМЕР 	  	    | ЧТО ДЕЛАЕТ |
| ------       	       	    | ------					     |
|  **Добавления:**           |						     |
|  `xs incl x`<br>или `xs + x`                 |Множество содержащее все элементы `xs` а также элемент `x`.|
|  **Удаления:**               |						     |
|  `xs excl x`<br>или `xs - x`  	            |Множество содержащее все элементы `xs` кроме `x`.|
|  `xs removedAll ys`<br>или `xs -- ys`  	            |Множество содержащее все элементы `xs` кроме элементов `ys`.|

Изменяемые множества предоставляют в дополнение к перечисленным методам еще методы добавления, удаления или обновления элементов.

### Операции на Классе mutable.Set ###

| ПРИМЕР  	  	    | ЧТО ДЕЛАЕТ				     |
| ------       	       	    | ------					     |
|  **Добавления:**           |						     |
|  `xs addOne x`<br>или `xs += x`  	            |Добавляет элемент `x` во множество `xs` побочным эффектом и возвращает сам `xs`. |
|  `xs addAll ys`<br>или `xs ++= ys`  	    |Добавляет все элементы `ys` во множество `xs` побочным эффектом и возвращает сам `xs`. |
|  `xs add x`  	            |Добавляет элемент `x` к `xs` и возвращает `true`, если `x` ранее не содержался в множестве, `false` если был.|
|  **Удаления:**            |						     |
|  `xs subtractOne x`<br>или `xs -= x`  	            |Удаляет элемент `x` из множества `xs` побочным эффектом и возвращает сам `xs`.|
|  `xs subtractAll ys`<br>или `xs --= ys`  	    |Удаляет все элементы `ys` из множества `xs` побочным эффектом и возвращает сам `xs`. |
|  `xs remove x`  	    |Удаляет элемент `x` из `xs` и возвращает `true`, если `x` ранее не содержался в множестве, `false` если был.|
|  `xs filterInPlace p`  	    |Оставляет только те элементы в `xs` которые удовлетворяют условию `p`.|
|  `xs.clear()`  	    |Удаляет все элементы из `xs`.|
|  **Обновления:**              |						     |
|  `xs(x) = b`  	    |(тоже самое что и `xs.update(x, b)`). Если логический аргумент `b` равен `true`, то добавляет `x` к `xs`, иначе удаляет `x` из `xs`.|
|  **Клонирования:**             |						     |
|  `xs.clone`  	            |Создает новое мутабельное множество с такими же элементами как у `xs`.|

Операции `s += elem` добавляют элемент `elem` к множеству `s` в качестве сайд эффекта, возвращая в качестве результата мутабельное множество. Точно так же, `s -= elem` удаляет `elem` из множества, и возвращает это множество в качестве результата. Помимо `+=` и `-=` есть еще пакетные операции `++=` и `--=` которые добавляют или удаляют все элементы итерируемой коллекции.

Выбор в качестве имен методов `+=` и `-=` будет означать для вас, то что схожий код сможет работать как с изменяемыми, так и с неизменяемыми множествами. Сначала рассмотрим следующий пример в консоле, в котором используется неизменяемый набор параметров `s`:

    scala> var s = Set(1, 2, 3)
    s: scala.collection.immutable.Set[Int] = Set(1, 2, 3)
    scala> s += 4
    scala> s -= 2
    scala> s
    res2: scala.collection.immutable.Set[Int] = Set(1, 3, 4)

Мы использовали `+=` и `-=` на `var` типа `immutable.Set`. Выражение `s += 4` является сокращение для `s = s + 4`. Тоесть вызов метода сложения `+` на множестве `s`, а затем присвоения результата обратно в переменную `s` . Рассмотрим теперь аналогичные действия с изменяемым множеством. 


    scala> val s = collection.mutable.Set(1, 2, 3)
    s: scala.collection.mutable.Set[Int] = Set(1, 2, 3)
    scala> s += 4
    res3: s.type = Set(1, 4, 2, 3)
    scala> s -= 2
    res4: s.type = Set(1, 4, 3)

Конечный эффект очень похож на предыдущий результат; мы начали с `Set(1, 2, 3)` закончили с `Set(1, 3, 4)`. Несмотря на то, что выражения выглядят так же, но работают они несколько иначе. `s += 4` теперь вызывает метод `+=` на изменяемом множестве `s`, измененяет свое собственное значение. По схожей схеме работает, `s -= 2` вызывая метод `-=` на томже самом множестве.

Сравнение этих двух подходов демонстрирует важный принцип. Часто можно заменить изменяемую коллекцию, хранящуюся в `val`, неизменяемой коллекцией, хранящейся в `var`, и _наоборот_. Это работает, по крайней мере, до тех пор, пока нет прямых отсылок на коллекцию, используя которую можно было бы определить была ли коллекция обновлена или создана заново.

У изменяемых множеств также есть операции `add` и `remove` как эквиваленты для `+=` и `-=`. Разница лишь в том, что команды `add` и `remove` возвращают логический результат, показывающий, повлияла ли операция на само множество или нет.

Текущая реализация изменяемого множества по умолчанию использует хэш-таблицу для хранения элементов множества. Реализация неизменяемого множества по умолчанию использует представление, которое адаптируется к количеству элементов множества. Пустое множество представлено объектом сингэлтоном. Множества размеров до четырех представлены одним объектом, в котором все элементы хранятся в виде полей. За пределами этого размера, неизменяемые множества реализованны в виде [Сжатого Отображенния Префиксного Дерева на Ассоциативном Массиве]({% link _ru/overviews/collections-2.13/concrete-immutable-collection-classes.md %}).

Результатом такой схемы представления является то, что неизменяемые множества малых размеров (скажем, до 4), более компактны и более эффективны, чем изменяемые. Поэтому, если вы ожидаете, что размер множества будет небольшим, постарайтесь сделать его неизменяемым.

Два дочерних трейта множеств `SortedSet` и `BitSet`.

### Отсортированное Множество (SortedSet) ###
[SortedSet](https://www.scala-lang.org/api/current/scala/collection/SortedSet.html) это множество, которое отдает свои элементы (используя `iterator` или `foreach`) в заданном порядке (который можно свободно задать в момент создания множества). Стандартное представление [SortedSet](https://www.scala-lang.org/api/current/scala/collection/SortedSet.html) - это упорядоченное двоичное дерево, которое поддерживает свойство того, что все элементы левого поддерева меньше, чем все элементы правого поддерева. Таким образом, простой упорядоченный обход может вернуть все элементы дерева в возрастающем порядке. Scala класс [immutable.TreeSet](https://www.scala-lang.org/api/current/scala/collection/immutable/TreeSet.html) базируется на _красно-черном_ дереве, в котором сохраняется тоже свойство но при этом само дерево является _сбалансированным_ --, то есть все пути от корня дерева до листа имеют длину, которая может отличаться друг от друга максимум на еденицу.

При создании пустого [TreeSet](https://www.scala-lang.org/api/current/scala/collection/immutable/TreeSet.html), можно сначала указать требуемый порядок:

    scala> val myOrdering = Ordering.fromLessThan[String](_ > _)
    myOrdering: scala.math.Ordering[String] = ...

Затем, чтоб создать пустой TreeSet с определенным порядком, используйте:

    scala> TreeSet.empty(myOrdering)
    res1: scala.collection.immutable.TreeSet[String] = TreeSet()

Или можно опустить указание аргумента с функцией сравнения, но указать тип элементов множества. В таком случае будет использоваться порядок заданный по умолчанию на данном типе.   

    scala> TreeSet.empty[String]
    res2: scala.collection.immutable.TreeSet[String] = TreeSet()

Если вы создаете новое множество из существующего упорядоченного множества (например, путем объединения или фильтрации), оно будет иметь туже схему упорядочения элементов, что и исходное множество. Например

    scala> res2 + "one" + "two" + "three" + "four"
    res3: scala.collection.immutable.TreeSet[String] = TreeSet(four, one, three, two)

Упорядоченные множества также поддерживают запросы на диапазоны. Например, метод `range` возвращает все элементы от _начального_ элемента до _конечного_, но исключая конечный элемент. Или же метод `from` возвращает все элементы от _начального_ и далее все остальные элементы в порядке очередности. Результатом работы обоих методов также будет упорядоченное множество. Примеры:

    scala> res3.range("one", "two")
    res4: scala.collection.immutable.TreeSet[String] = TreeSet(one, three)
    scala> res3 rangeFrom "three"
    res5: scala.collection.immutable.TreeSet[String] = TreeSet(three, two)


### Битовые Наборы (BitSet) ###

Битовые Наборы - это множество неотрицательных целочисленных элементов, которые упаковываются в пакеты.  Внутреннее представление [BitSet](https://www.scala-lang.org/api/current/scala/collection/BitSet.html) использует массив `Long`ов. Первый `Long` охватывает элементы от 0 до 63, второй от 64 до 127 и так далее (Неизменяемые наборы элементов в диапазоне от 0 до 127 оптимизированны таким образом что хранят биты непосредственно в одном или двух полях типа `Long` без использования массива). Для каждого `Long` 64 бита каждого из них устанавливается значение 1, если соответствующий элемент содержится в наборе, и сбрасывается в 0 в противном случае. Отсюда следует, что размер битового набора зависит от размера самого большого числа, которое в нем хранится. Если `N` является самым большим размером числа, то размер набора будет составлять `N/64` от размера `Long`, или `N/8` байта плюс небольшое количество дополнительных байт для информации о состоянии.

Поэтому битовые наборы компактнее, чем другие множества, когда речь идет о хранении мелких элементов. Еще одним преимуществом битовых наборов является то, что такие операции, как проверка на наличие элемента `contains`, добавление либо удаление элементов с `+=` и `-=` черезвычайно эффективны.

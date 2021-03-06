Введение

Подобно стекам, очередь — хранит элемент последовательным образом. Существенное отличие от стека – использование FIFO (First in First Out) вместо LIFO. Принцип работы очереди можно наглядно показать на примере кольцевого буфера. Когда элементы, добавляемые в конец очереди и извлекаемые из очереди расположена по кольцу.

Постановка задачи

Цель данной работы — разработка графического приложения на основе очереди, которое должно отображать добавление и извлечение элементов из очереди.

Руководство пользователя

После запуска программы необходимо задать максимальный размер очереди, начальный размер очереди, вероятность добавления элемента и вероятность извлечения элемента. Затем нужно нажать на кнопку «Пуск». Программа начнет рисовать кольцо, соответствующее добавлению и извлечению элементов.

Руководство программиста
Описание структуры программы

Программа содержит два класса:
•	Form1 – стандартный класс windows формы, который содержит все графические элементы программы
•	TQueue – класс очереди. Используется один из двух вариантов очереди:
o	очередь на основе массива
o	очередь на основе списка

После запуска программы и ввода всех необходимых данных создаётся очередь и в ней добавляются и извлекаются (в зависимости от заданных вероятностей) случайные элементы. Графическая функция строит соответствующие дуги, которые визуализирую процесс добавления и извлечения элементов.

Описание структур данных
Класс TQueue на массивах (шаблонный)
Поля:
•	mas - массив элементов указанного типа
•	MaxSize – максимальное количество элементов массива
•	Head, Tail –  голова и хвост очереди, т.е. начальный и конечный элементы очереди
•	CurrSize – текущий размер очереди
Методы:
•	operator= - оператор присваивания
•	IsEmpty – проверка очереди на пустоту
•	IsFull – проверка очереди на переполнение
•	Push – положить элемент в очередь
•	Pop – взять элемент из очереди
•	Front – посмотреть, что в начале очереди
•	Back – посмотреть, что в конце очереди
•	GetHead – возвращает начальный элемент
•	GetMaxSize – возвращает максимальный размер
•	GetSize – возвращает текущий размер очереди

Класс TQueue на списках (шаблонный)
Поля:
•	структура pFirst, которая имеет два поля:
o	val – значение
o	pNext – указатель на следующий элемент
•	структура pLast, которая имеет два поля:
o	val – значение
o	pNext – указатель на следующий элемент

Методы:
•	operator= - оператор присваивания
•	IsEmpty – проверка очереди на пустоту
•	IsFull – проверка очереди на переполнение
•	Push – положить элемент в очередь
•	Pop – взять элемент из очереди
•	Front – посмотреть, что в начале очереди
•	Back – посмотреть, что в конце очереди
•	GetHead – возвращает 0
•	GetMaxSize – возвращает 10000
•	GetSize – возвращает текущий размер очереди
•	Clear – очищает очередь

Описание алгоритмов

Методы  TQueue на массивах

operator= - оператор присваивания
Позволяет присвоить очередь. Сначала присваивается максимальный размер, затем создаётся новый массив такого размера. После этого присваивается голова, хвост и текущий размер очереди. Если голова меньше хвоста, то в цикле от головы до хвоста присваивается массив поэлементно. Если голова больше хвоста, то сначала такой цикл запускается от головы до конца очереди, а потом от 0 до хвоста.

IsEmpty – проверка очереди на пустоту
Возвращает true,  если текущий размер очереди равен 0.

IsFull – проверка очереди на переполнение
Возвращает true, если текущий размер равен максимальному.

Push – положить элемент в очередь
Позволяет добавить элемент в очередь. Если хвост очереди не находится в конце, то элементу массива с индексом хвоста присваивается значение, а хвост увеличивается на единицу. В противном случае хвост обнуляется, и элементу массива с индексом хвоста присваивается значение.

Pop – взять элемент из очереди
Записывается индекс головы. Затем если голова не стоит в конце, то она  увеличивается на единицу, в противном случае она обнуляется. Возвращается элемент с запомненной в начала позиции.

Front – посмотреть, что в начале очереди
Возвращается элемент массива с индексом головы.

Back – посмотреть, что в конце очереди
Возвращается элемент массива с индексом хвоста.

Методы  TQueue на списках

operator= - оператор присваивания
Сначала очередь очищается с помощью метода Clear. Затем создаётся временная структура и ей присваивается pFirst присваиваемой очереди. Затем в цикле пока указатель pFirst этой временной структуры не будет показывать на NULL, присваивается значение с помощью метода Push и указатель перенаправляется на следующий.

IsEmpty – проверка очереди на пустоту
Возвращает true, если pFirst указывает на NULL.

IsFull – проверка очереди на переполнение
Создаётся временная структура. Если её указатель показывает на NULL, то возвращается true (1), в противном случае возвращается 0 (false).

Push – положить элемент в очередь
Если очередь не полная, создаётся новый элемент. Ему присваивается значение, а его указатель pNext направляется на NULL. Затем, если текущий pLast не показывает на NULL, то его pNext направляют на временный элемент, и этот элемент становится последним. В противном случае (если до этого очередь была пустая) этот элемент становится сразу и первым и последним.

Pop – взять элемент из очереди
Если очередь не пустая, создаётся переменная, и ей присваивается значение первого элемента из очереди. Затем создаётся временный элемент и ему присваивается первый. После чего указатель pFirst перенаправляется на следующий (второй) элемент очереди. Временный элемент удаляется, а переменная со значением возвращается.

Front – посмотреть, что в начале очереди
Возвращается значение первого элемента.

Back – посмотреть, что в конце очереди
Возвращается значение последнего элемента.

GetSize – возвращает текущий размер очереди
Создаётся структура и ей присваивается pFirst  и вводится счётчик. В цикле, пока временный указатель не будет указывать на NULL, увеличивается счётчик на единицу и этот указатель перенаправляется на следующий элемент. Возвращается значение счётчика после такого цикла.

Clear – очищает очередь
Создается временный элемент. В цикле, пока указатель на первый элемент не будет показывать на NULL, pFirst перенаправляется на следующий, временный элемент удаляется и ему присваивается текущий первый.

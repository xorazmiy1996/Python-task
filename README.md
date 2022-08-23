# Python-task



<details>
  <summary>Задания 1</summary>

На языке Python реализовать алгоритм (функцию) определения четности целого числа, который будет аналогичен нижеприведенному по функциональности, но отличен по своей сути. Объяснить плюсы и минусы обеих реализаций.


    def isEven(value):return value%2==0 
    

Отвечать:[ссылка]()

    def is_even(number): return number & 1    

Давайте обратимся к результирующему коду на ассемблере для обеих функций, для начала используем GCC 9.3 на сайте godbolt:
        
        def isEven():

        1     0 LOAD_CONST               0 (<code object isEven at 0x564ab172e8f0, file "example.py", line 1>)
              2 LOAD_CONST               1 ('isEven')
              4 MAKE_FUNCTION            0
              6 STORE_NAME               0 (isEven)
              8 LOAD_CONST               2 (None)
             10 RETURN_VALUE

          Disassembly of <code object isEven at 0x564ab172e8f0, file "example.py", line 1>:
        1     0 LOAD_FAST                0 (value)
              2 LOAD_CONST               1 (2)
              4 BINARY_MODULO
              6 LOAD_CONST               2 (0)
              8 COMPARE_OP               2 (==)
             10 RETURN_VALUE
        
        def is_even():

        1     0 LOAD_CONST               0 (<code object is_even at 0x55ad0475f240, file "example.py", line 1>)
              2 LOAD_CONST               1 ('is_even')
              4 MAKE_FUNCTION            0
              6 STORE_NAME               0 (is_even)
              8 LOAD_CONST               2 (None)
             10 RETURN_VALUE
          Disassembly of <code object is_even at 0x55ad0475f240, file "example.py", line 1>:
        1     0 LOAD_FAST                0 (number)
              2 LOAD_CONST               1 (1)
              4 BINARY_AND
              6 RETURN_VALUE
И вот здесь уже есть разница.Функция is_even() работает быстрее, чем функция isEven().   
        
        
        



</details>


<details>
  <summary>Задания 2</summary>

На языках Python(2.7)  написать минимум по 2 класса реализовывающих циклический буфер FIFO.

Объяснить плюсы и минусы каждой реализации.

Отвечать:

Первая реализация:

    class RingBuffer:
    def __init__(self,size_max):
        self.max = size_max
        self.data = []

    class __Full:
        def append(self, x):
            self.data[self.cur] = x
            self.cur = (self.cur+1) % self.max
        def get(self):
            return self.data[self.cur:]+self.data[:self.cur]

    def append(self,x):
        self.data.append(x)
        if len(self.data) == self.max:
            self.cur = 0
            self.__class__ = self.__Full

    def get(self):
        return self.data
Вторая реализация:
    
    class CircularBuffer(object):
    def __init__(self, size):
        self.index= 0
        self.size= size
        self._data = []

    def record(self, value):
        if len(self._data) == self.size:
            self._data[self.index]= value
        else:
            self._data.append(value)
        self.index= (self.index + 1) % self.size

    def __getitem__(self, key):
        return(self._data[key])

    def __repr__(self):
        return self._data.__repr__() + ' (' + str(len(self._data))+' items)'

    def get_all(self):
        return(self._data)


</details>

<details>
  <summary>Задания 3</summary>

На языке Python реализовать функцию, которая быстрее всего (по процессорным тикам) отсортирует данный ей массив чисел. Массив может быть любого размера со случайным порядком чисел (в том числе и отсортированным). Объяснить почему вы считаете, что функция соответствует заданным критериям.

Отвечать:


    def qsort(array):
            if len(array) < 2:
                return array
            else:
                pivot = array.pop(randrange(len(array)))
                small = [i for i in array if i <= pivot]
                big = [i for i in array if i > pivot]
                return qsort(small) + [pivot] + qsort(big)

Big O : O(nlogn) для qsort

    
        
[ссылка]()

</details>


Numpy Giriş
===

## Diziler
Numpy dizisi, tümü aynı türde olan bir değerler sistemidir ve negatif olmayan tam sayıların bir dizini tarafından dizine eklenir. Boyutların sayısı, dizinin sıralamasıdır; Bir dizinin şekli, her boyut boyunca dizinin boyutunu veren bir tam sayı dizisidir.

İç içe Python listelerinden sayısal dizileri başlatabilir ve köşeli parantez kullanarak elemanlara erişebiliriz:


```python
import numpy as np

a = np.array([1, 2, 3])   # 1 dizi oluşturma
print(type(a))            # "<class 'numpy.ndarray'>" yazdırır
print(a.shape)            # "(3,)" yazdırır
print(a[0], a[1], a[2])   # "1 2 3" yazdırır
a[0] = 5                  # Dizinin bir öğesini değiştirme
print(a)                  # "[5, 2, 3]" yazdırır

b = np.array([[1, 2, 3], [4, 5, 6]])    # 2 dizi oluşturma
print(b.shape)                     #  "(2, 3)" yazdırır
print(b[0, 0], b[0, 1], b[1, 0])   # "1 2 4" yazdırır
```

    <class 'numpy.ndarray'>
    (3,)
    1 2 3
    [5 2 3]
    (2, 3)
    1 2 4
    

Numpy ayrıca diziler oluşturmak için birçok işlev sunar:


```python
a = np.zeros((2, 2))   # Tüm sıfırlardan bir dizi oluşturun
print(a)              # yazdır: "[[ 0.  0.]
                      #          [ 0.  0.]]"

b = np.ones((1, 2))    # Hepsinden oluşan bir dizi oluşturun
print(b)              # yazdır: "[[ 1.  1.]]"

c = np.full((2, 2), 7)  # Sabit bir dizi oluşturun
print(c)               # yazdır: "[[ 7.  7.]
                       #          [ 7.  7.]]"

d = np.eye(2)         # 2x2 kimlik matrisi oluşturun
print(d)              # yazdır :"[[ 1.  0.]
                      #          [ 0.  1.]]"

e = np.random.random((2, 2))  # Rasgele değerlerle dolu bir dizi oluşturma
print(e)                     # Yazdır: "[[0.78444834 0.31119597]
                             #               [0.446503   0.55623441]]"
```

    [[0. 0.]
     [0. 0.]]
    [[1. 1.]]
    [[7 7]
     [7 7]]
    [[1. 0.]
     [0. 1.]]
    [[0.78444834 0.31119597]
     [0.446503   0.55623441]]
    

## Dizi Oluşturma


```python
# Aşağıdaki sırada 2. sırayı  (3, 4) şeklinde oluşturun
# [[ 1  2  3  4]
#  [ 5  6  7  8]
#  [ 9 10 11 12]]
a = np.array([[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]])

# İlk 2 satırdan oluşan alt diziyi çıkarmak için dilimleme kullanın
# ve sütun 1 ve 2; b aşağıdaki şekil dizisidir (2, 2):
# [[2 3]
#  [6 7]]
b = a[:2, 1:3]

# Bir dizinin bir dilimi, aynı verilere bir görünümdür;
# orijinal diziyi değiştirir.
print(a[0, 1])   # yazdır: "2"
b[0, 0] = 77     # b [0, 0], [0, 1] ile aynı veri parçasıdır
print(a[0, 1])   # yazdır : "77"
```

    2
    77
    

## Dizi Veri Türleri


```python
x = np.array([1, 2])   # Numpy veri tipini seçsin
print(x.dtype)         # yazdır "int64"

x = np.array([1.0, 2.0])   #Numpy veri tipini seçsin
print(x.dtype)             # yazdır "float64"

x = np.array([1, 2], dtype=np.int64)   # Belirli bir veri tipini zorla
print(x.dtype)                         # yazdır "int64"
```

    int32
    float64
    int64
    

## iŞLEMLER


```python
x = np.array([[1, 2], [3, 4]], dtype=np.float64)
y = np.array([[5, 6], [7, 8]], dtype=np.float64)

#  elementwise  toplam; her ikisi de diziyi üretir
# [[ 6.0  8.0]
#  [10.0 12.0]]
print(x + y)
print(np.add(x, y))

# yatay yönde fark; her ikisi de diziyi üretir
# [[-4.0 -4.0]
#  [-4.0 -4.0]]
print(x - y)
print(np.subtract(x, y))

# elementwise  ürün; her ikisi de diziyi üretir
# [[ 5.0 12.0]
#  [21.0 32.0]]
print(x * y)
print(np.multiply(x, y))

# elementwise  bölünmesi; her ikisi de diziyi üretir
# [[ 0.2         0.33333333]
#  [ 0.42857143  0.5       ]]
print(x / y)
print(np.divide(x, y))

# elementwise  karekök; dizi üretir
# [[ 1.          1.41421356]
#  [ 1.73205081  2.        ]]
print(np.sqrt(x))

# Maksimum değerin dizi dizinini döndür
print(np.argmax(x))

# Satır başına maksimum değerlerin dizi endekslerini döndür
print(np.argmax(x, axis=1))

# Sütun başına maksimum değerlerin dizi endekslerini döndür
print(np.argmax(x, axis=0))
```

    [[ 6.  8.]
     [10. 12.]]
    [[ 6.  8.]
     [10. 12.]]
    [[-4. -4.]
     [-4. -4.]]
    [[-4. -4.]
     [-4. -4.]]
    [[ 5. 12.]
     [21. 32.]]
    [[ 5. 12.]
     [21. 32.]]
    [[0.2        0.33333333]
     [0.42857143 0.5       ]]
    [[0.2        0.33333333]
     [0.42857143 0.5       ]]
    [[1.         1.41421356]
     [1.73205081 2.        ]]
    3
    [1 1]
    [1 1]
    

MATLAB'ın aksine, `*` öğesinin matris çarpımı değil, elementwise çarpma olduğunu unutmayın. Bunun yerine, vektörlerin iç ürünlerini hesaplamak, bir vektörü bir matrisle çarpmak ve matrisleri çarpmak için `dot` işlevini kullanırız. `dot`, hem numpy modülündeki bir fonksiyon olarak hem de array nesnelerinin bir örnek metodu olarak kullanılabilir:


```python
x = np.array([[1, 2], [3, 4]])
y = np.array([[5, 6], [7, 8]])

v = np.array([9, 10])
w = np.array([11, 12])

# Vektörlerin İç çarpımı; her ikisi de 219
print(v.dot(w))
print(np.dot(v, w))

# Matris / vektör ürünü; her ikisi de rütbe 1 dizisini üretmektedir [29 67]
print(x.dot(v))
print(np.dot(x, v))

# Matris / matris ürünü; her ikisi de rank 2 dizisini üretir
# [[19 22]
#  [43 50]]
print(x.dot(y))
print(np.dot(x, y))
```

    219
    219
    [29 67]
    [29 67]
    [[19 22]
     [43 50]]
    [[19 22]
     [43 50]]
    

NumPy, dizilerde hesaplamalar yapmak için birçok yararlı işlev sunar; en kullanışlı olanlardan biri toplamıdır:


```python
x = np.array([[1, 2],[3, 4]])

print(np.sum(x))  # Tüm elemanların toplamını hesapla; "10" yazdırıyor
print(np.sum(x, axis=0))  # Her sütunun toplamını hesapla; "[4 6]" yazdırıyor
print(np.sum(x, axis=1))  # Her satırın toplamını hesapla; "[3 7]" yazdırıyor
```

    10
    [4 6]
    [3 7]
    

## Yineleme

NumPy dizileri üzerinde yineleme yapmak için, bir listeyi yineleniyormuş gibi yapabilirsiniz


```python
a = np.array([1, 4, 5, 10, 12, 15], int)

for number in a:
    print(number)
```

    1
    4
    5
    10
    12
    15
    

## İlişkisel Operatörler


```python
# Rasgele tamsayı değerlerine sahip diziler oluşturma
a = np.random.randint(10, size=(5))
b = np.random.randint(10, size=(5))

print('a:', a)
print('b:', b)
print(a > b)
print(a < b)
print(a == b)
print(a >= b)
print(a <= b)
print(a != b)

print(np.equal(a, b))
```

    a: [1 8 6 9 0]
    b: [5 2 9 0 6]
    [False  True False  True False]
    [ True False  True False  True]
    [False False False False False]
    [False  True False  True False]
    [ True False  True False  True]
    [ True  True  True  True  True]
    [False False False False False]
    


```python

```

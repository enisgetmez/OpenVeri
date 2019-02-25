
OpenCV'ye Başlarken
===

## Görüntü Okumak

Bir görüntüyü okumak için `cv2.imread ()` işlevini kullanırız.


```python
import cv2
import numpy as np
```


```python
# ilk argüman yüklenecek resimdir
# 2. argüman argümanı görüntünün rengidir
     # cv2.IMREAD_COLOR renkli bir resim yükler
     # cv2.IMREAD_GRAYSCALE görüntüyü gri tonlamalı olarak yükler
image = cv2.imread('../assets/resim.jpg', cv2.IMREAD_COLOR)
```

## Bir Görüntüyü Görüntülemek

Bir resmi görüntülemek için `cv2.imshow ()` işlevini kullanırız.


```python
cv2.imshow('image', image)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

`cv2.waitKey ()` bir klavye bağlama işlevidir; bu, herhangi bir klavye olayı için belirli bir süre (milisaniye cinsinden) beklediği anlamına gelir. Zaman içerisinde herhangi bir tuşa basıldığında program devam eder. Eğer “0” geçerse, süresiz olarak bekler.

`cv2.destroyAllWindows ()`, oluşturulan tüm pencereleri yok eder. Belirli bir pencereyi silmek için, argüman olarak geçirilen pencere ismiyle `cv2.destroyWindow ()` kullanın.


```python
cv2.namedWindow('image', cv2.WINDOW_NORMAL)
cv2.imshow('image', image)
cv2.waitKey(0)
cv2.destroyWindow('image')
```

`cv2.namedWindow()` bir görüntünün yüklenebileceği bir pencere oluşturur. Pencerenin yeniden boyutlandırılabilir olup olmadığı belirtilebilir. Varsayılan bayrak `cv2.WINDOW_AUTOSIZE` dır. Bu arada, bayrağı `cv2.WINDOW_NORMAL` olarak belirtirseniz, pencere yeniden boyutlandırılabilir.

## Görüntüyü Kaydetmek

Bir görüntüyü kaydetmek için `cv2.imwrite()` işlevini kullanırız.

İlk argüman dosya adı, ikincisi ise kaydedilecek resimdir.


```python
image = cv2.imread('../assets/enis.jpg', cv2.IMREAD_GRAYSCALE)
cv2.imwrite('enis_grayscale.jpg', image)
```




    True



## Özet

Resmimizi gri tonlamalı olarak yükleyelim, görüntüleyelim, sonra kaydedelim.


```python
image = cv2.imread('../assets/enis.jpg', cv2.IMREAD_GRAYSCALE)
cv2.imshow('image', image)

k = cv2.waitKey(0)

if k == 27:    # esc tuşuna basınca çıkış yapılır
    cv2.destroyAllWindows()
elif k == ord('s'):    # s tuşuna basılırsa görüntü kaydedilip çıkış yapılır
    cv2.imwrite('enis_grayscale.jpg', image)
    cv2.destroyAllWindows()
```

## OpenCV’de video

### Kameradan Video Çekme

Bir video çekmek için bir `cv2.VideoCapture` nesnesi oluşturmamız gerekiyor. Bunun argümanı cihaz dizini veya bir video dosyasının adı olabilir.


```python
import cv2
import numpy as np

cap = cv2.VideoCapture(0) #kameranın bağlı olduğu port

while True:
    
    _, frame = cap.read()
    
    cv2.imshow('webcam', frame) # kamerayı göster
    
    if cv2.waitKey(1) == 27:
        break
        
cap.release()
cv2.destroyAllWindows()
```

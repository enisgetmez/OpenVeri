# Core \(Çekirdek\) İşlemleri

## OpenCV'de Core\(Çekirdek\) İşlemleri

resimlerin içinde bulunan temel ve aritmetik işlemleri öğreniriz.

```python
import cv2
import numpy as np
```

### Görüntü Özelliklerine Erişim

Bir görüntünün şekline bir diziye erişiyormuş gibi erişilebilir, `image.shape`. Görüntü bir gri tonlama değilse, satır, sütun ve kanal sayısının bir demetini döndürür.

```python
image = cv2.imread('../assets/enis.jpg')

print(image.shape)
```

```text
(1182, 1000, 3)
```

Görüntü gri tonluysa, yalnızca `ROWxCOL` döndürür. Bu nedenle, görüntünün gri tonlamalı veya renkli olup olmadığını kontrol etmek için kullanılabilir.

Toplam piksel sayısını elde etmek için.

```python
print(image.size)
```

```text
3546000
```

Görüntü veri tipini almak için.

```python
print(image.dtype)
```

```text
uint8
```

### Piksel Değerlerine Erişim ve Değiştirme

Bir piksel değerine satır ve sütun koordinatlarıyla erişebiliriz. RGB görüntüsü için, Mavi, Yeşil, Kırmızı değerleri dizisini döndürür. Gri tonlamalı görüntü için, sadece karşılık gelen yoğunluk döndürülür.

```python
pixel = image[261, 302]
```

```python
print(pixel)
```

```text
[157 187 236]
```

```python
# yalnızca mavi piksele erişmek
print(pixel[0])

# yalnızca yeşil piksele erişmek
print(pixel[1])

# yalnızca kırmızı piksele erişmek
print(pixel[2])
```

```text
157
187
236
```

```python
cv2.imshow('pixel', pixel)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

```python
pixel = 0

cv2.imshow('pixel', pixel)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

### İlgi Bölgesi

```python
# sadece insan yüzüne ait piksel bölgelerine erişmek
kırp = image[302:(302 + 322), 261:(261 + 339)]
```

```python
cv2.namedWindow('image', cv2.WINDOW_NORMAL)
cv2.namedWindow('kırpılmış', cv2.WINDOW_NORMAL)
cv2.imshow('image', image)
cv2.imshow('kırpılmış', kırp)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

```python
from_center = False
region = cv2.selectROI(image, from_center)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

```python
print(region)
```

```text
(261, 285, 344, 376)
```

```python
kırp = image[region[1]:(region[1] + region[3]), region[0]:(region[0] + region[2])]
```

```python
cv2.namedWindow('image', cv2.WINDOW_NORMAL)
cv2.namedWindow('kırpılmış', cv2.WINDOW_NORMAL)
cv2.imshow('image', image)
cv2.imshow('kırpılmış', kırp)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

### Görüntü Kanallarını Bölme ve Birleştirme

RGB kanalları gerektiğinde kendi düzlemlerine ayrılabilir. Yine RGB oluşturmak için de birleştirilebilir.

```python
mavi, yesil, kirmizi = cv2.split(image)
```

```python
cv2.imshow('mavi_kanal', mavi)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

```python
cv2.imshow('kırmızı_kanal', kirmizi)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

```python
cv2.imshow('yeşil_kanal', yesil)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

```python
image = cv2.merge((mavi, yesil, kirmizi))

cv2.imshow('merged_back', image)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

`Cv2.split()`ve `cv2.merge()`kullanmak hesaplama açısından zordur,bunun yerine NumPy dilimlemeyi kullanabiliriz.

```python
mavi = image[:, :, 0]

cv2.imshow('mavi_kanal', mavi)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

```python
yesil = image[:, :, 1]

cv2.imshow('yeşil_kanal', yesil)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

```python
kirmizi = image[:, :, 2]

cv2.imshow('kırmızı_kanal', red)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

NumPy dilimlemeyi bir görüntü kanalına erişmenin bir yolu olarak da kullanabiliriz.

```python
# kırmızı kanalı değiştir
image[:, :, 2] = 0

cv2.imshow('modified_kırmızı_kanal', image)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

### Resim Ekleme

`Cv2.add ()` kullanarak görüntüleri ekleyebiliriz. Ancak her iki görüntünün de aynı boyutta olması gerekir.

```python
enis = cv2.imread('../assets/enis.jpg')
ali = cv2.imread('../assets/ali.png')
```

```python
enis_ali = cv2.add(enis, ali)

cv2.imshow('ekle', enis_ali)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

### Görüntü karıştırma

Bu aynı zamanda görüntü eklemedir, ancak görüntülere verilen farklı ağırlıklar vardır. Denklem aşağıdaki gibidir

$$g(x) = (1 - \alpha)\ f_{0}(x) + \alpha\ f_{1}(x)$$

$  Alpha $ değerini 0 $  rightarrow $ 1 ile değiştirerek, görüntüler arasında bir "geçiş hissi" verir.

Örneğimize göre, birlikte harmanlamak için iki resim çekiyoruz. İlk görüntüye 0.7, ikinci görüntüye 0.3 ağırlık atarız. `Cv2.addWeighted ()` kullanarak aşağıdaki denklemi uygular

$$dst = \alpha \cdot img1 + \beta \cdot img2 + \gamma$$

```python
blend = cv2.addWeighted(enis, 0.7, ali, 0.3, 0)
```

```python
cv2.imshow('blend', blend)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

### Bitsel İşlem

```python
# kullanılacak logoyu yükle
artificaid = cv2.imread('../assets/artificaid.jpg')
```

```python
# logo şeklini göster
print(artificaid.shape)
```

```text
(823, 638, 3)
```

```python
# Enis resminin bir şekli olduğunu bilerek # (1182, 1000, 3)
# logo resim için oldukça büyük
# yeniden boyutlandıralım
artificaid = cv2.resize(artificaid, (int(artificaid.shape[1] * 0.25), int(artificaid.shape[0] * 0.25)))
```

```python
print(artificaid.shape)
```

```text
(205, 159, 3)
```

```python
# logo özelliklerini almak
rows, cols, channels = artificaid.shape
```

```python
# logoyu sol üst köşeye koyalım
roi = enis[0:rows, 0:cols]

cv2.imshow('roi', roi)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

```python
# logonun maskesini oluştur

#, eşikleme için görüntüyü gri tonlamaya dönüştürür
artificaid_gray = cv2.cvtColor(artificaid, cv2.COLOR_BGR2GRAY)

# ilk argüman kaynak görüntüdür
# second argümanı eşik değeridir
# üçüncü değişken eşiğe ulaşıldığında kullanılacak değerdir
# cv2.THRESH_BINARY_INV, üçüncü argümanın durumunu tersine çevirir
ret, mask = cv2.threshold(artificaid_gray, 220, 255, cv2.THRESH_BINARY_INV)

cv2.imshow('mask', mask)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

```python
#ters maske yarat
mask_inv = cv2.bitwise_not(mask)

cv2.imshow('mask_inv', mask_inv)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

```python
#logo alanını karartmak
enis_bg = cv2.bitwise_and(roi, roi, mask=mask_inv)

cv2.imshow('enis_bg', enis_bg)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

```python
# logo görüntüsünden logo bölgesini al
artificaid_fg = cv2.bitwise_and(artificaid, artificaid, mask=mask)

cv2.imshow('artificaid_fg', artificaid_fg)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

```python
# ilgilenilen bölgeye logo koymak
dst = cv2.add(enis_bg, enis_fg)
enis[0:rows, 0:cols] = dst

cv2.namedWindow('enis_artificaid', cv2.WINDOW_NORMAL)
cv2.imshow('enis_artificaid', enis)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

### Alıştırma

En iyi resminizi seçin, Artificaid'in logosunu buradan indirin: [https://tinyurl.com/artificaid](https://tinyurl.com/artificaid). Ardından, logoyu bit yönünde işlem kullanarak seçtiğiniz resime yerleştirin.

### Çizim İşlevleri Alıştırmaları

```python
artificaid = cv2.imread('../assets/Artificaid.jpg')

artificaid = cv2.resize(artificaid, (int(artificaid.shape[1] * 0.25), int(artificaid.shape[0] * 0.25)))

rows, cols, _ = artificaid.shape

cap = cv2.VideoCapture(0)

while True:
    ret, frame = cap.read()

    roi = frame[0:rows, 0:cols]

    artificaid_gray = cv2.cvtColor(artificaid, cv2.COLOR_BGR2GRAY)

    ret, mask = cv2.threshold(artificaid_gray, 220, 255, cv2.THRESH_BINARY_INV)
    mask_inv = cv2.bitwise_not(mask)

    frame_bg = cv2.bitwise_and(roi, roi, mask=mask_inv)
    artificaid_fg = cv2.bitwise_and(artificaid, artificaid, mask=mask)

    dst = cv2.add(frame_bg, artificaid_fg)
    frame[0:rows, 0:cols] = dst

    cv2.imshow('bitwise', frame)

    k = cv2.waitKey(1)

    if k == ord('q') or k == 27:
        cap.release()
        cv2.destroyAllWindows()
        break
```

### Görüntü Harmanlama Alıştırması

```python
enis = cv2.imread('../assets/Enis.jpg')

cap = cv2.VideoCapture(-1)

while True:
    _, frame = cap.read()
    rows, cols, _ = frame.shape
    enis = cv2.resize(enis, (int(cols), int(rows)))
    blend = cv2.addWeighted(frame, 0.8, enis, 0.2, 0)
    cv2.imshow('blend', blend)

    k = cv2.waitKey(1)

    if k == ord('q') or k == 27:
        cap.release()
        cv2.destroyAllWindows()
        break
```

### Kamera Filtreleme

```python
# web kamerası için VideoCapture nesnesi oluştur
cap = cv2.VideoCapture(0)

def apply_invert(frame):
    # ters görüntü döndür
    return cv2.bitwise_not(frame)

def apply_sepia(frame, intensity=0.5):
    blue = 20
    green = 66
    red = 112
    # sepia profilini kaplama olarak kullan
    frame = apply_color_overlay(frame, intensity=intensity, blue=blue, green=green, red=red)
    return frame

def verify_alpha_channel(frame):
    try:
        frame.shape[3]
    except IndexError:
        # çerçeveyi bir alpha kanalına dönüştürmek
        frame = cv2.cvtColor(frame, cv2.COLOR_BGR2BGRA)
    return frame

def apply_color_overlay(frame, intensity=0.5, blue=0, green=0, red=0):
    frame = verify_alpha_channel(frame)
    frame_height, frame_width, frame_channel = frame.shape
    sepia_bgra = (blue, green, red, 1)

    # Renk profiline göre kaplama oluşturmak (mavi, yeşil, kırmızı)
    overlay = np.full((frame_height, frame_width, 4), sepia_bgra, dtype='uint8')

    # Çerçeveye sepia ekle
    frame = cv2.addWeighted(overlay, intensity, frame, 1.0, 0)
    frame = cv2.cvtColor(frame, cv2.COLOR_BGRA2BGR)
    return frame

def alpha_blend(frame_1, frame_2, mask):
    # beyaz parçaları ayır
    alpha = mask / 255.0

    #  netliği ayarlaamk için arka planı bulanıklaştırmak
    blended = cv2.convertScaleAbs(frame_1 * (1 - alpha) + (frame_2 * alpha))

    return blended

def apply_portrait_mode(frame):
    frame = verify_alpha_channel(frame)

    # gri tonlamaya dönüştür
    gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)

     # 120 eşiğine dayalı bir maske oluşturun
     #, eğer bir piksel ulaşırsa veya 120'den büyükse,
     # 255 olması için değiştirin
    _, mask = cv2.threshold(gray, 120, 255, cv2.THRESH_BINARY)

    # alpha kanalına sahip maskeyi değiştir
    mask = cv2.cvtColor(mask, cv2.COLOR_GRAY2BGRA)

    # (21, 21) çekirdeği ile bulanıklaştırmak
    # 0 stddev
    blurred = cv2.GaussianBlur(frame, (21, 21), 0)

    # Orijinal çerçeveyi bulanık çerçeveyle harmanlayın
    # Odak nesnesini izole etmek için kullanmak maske ile
    blended = alpha_blend(frame, blurred, mask)

    # çerçeveyi BGR'ye dönüştür, yani alpha olmadan
    frame = cv2.cvtColor(blended, cv2.COLOR_BGRA2BGR)
    return frame

while True:
    ret, frame = cap.read()

    invert = apply_invert(frame)
    sepia = apply_sepia(frame)
    redish_color = apply_color_overlay(frame, intensity=0.5, red=230, blue=10)
    portrait_mode = apply_portrait_mode(frame)

    cv2.imshow('frame', frame)
    cv2.imshow('invert', invert)
    cv2.imshow('sepia', sepia)
    cv2.imshow('redish_color', redish_color)
    cv2.imshow('portrait_mode', portrait_mode)

    k = cv2.waitKey(1)

    if k == ord('q') or k == 27:
        cap.release()
        cv2.destroyAllWindows()
        break
```


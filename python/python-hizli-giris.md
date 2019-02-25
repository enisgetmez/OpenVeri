# Python Hızlı Giriş

## Temel Syntax

```python
print('Hello World!')
```

```text
Hello World!
```

```python
mesaj = 'Hello World!'
print(mesaj)
```

```text
Hello World!
```

## Kullanıcı Input / Output

```python
print('İsmin Ne?')
isim = input()
print('Selam,', isim)
```

```text
İsmin Ne?
Enis
Selam, Enis
```

```python
isim = input('İsmin Ne? ')
print('Selam,', isim)
```

```text
İsmin Ne? Enis
Selam, Enis
```

## Aritmetik Operatörler

```python
3 + 5
```

```text
8
```

```python
4 - 1
```

```text
3
```

```python
2 * 2
```

```text
4
```

```python
10 / 4 # Real Division (Türkçede gerçek bölüm diye geçiyor sanırım.) / Float çıktı verecek
```

```text
2.5
```

```python
10 // 5 # floor division(Tam Sayı) / Integer çıktı verecektir.
```

```text
2
```

```python
11 // 2
```

```text
5
```

```python
2 ** 3 # sayının üssünü verir yani 2nin 3. üssü
```

```text
8
```

```python
5 % 4 # modülü verir
```

```text
1
```

## Mantıksal Operatörler

```python
1 or 1
```

```text
1
```

```python
1 or 0
```

```text
1
```

```python
1 and 1
```

```text
1
```

```python
1 and 0
```

```text
0
```

```python
not True
```

```text
False
```

```python
not False
```

```text
True
```

## İlişkisel Operatör

```python
1 == 1 # Eşittir
```

```text
True
```

```python
0 == 1 # Eşittir
```

```text
False
```

```python
1 != 1 # Eşit Değildir
```

```text
False
```

```python
0 != 1 # Eşit Değildir
```

```text
True
```

```python
1 > 0 # Büyüktür / greater than
```

```text
True
```

```python
0 > 1 # Büyüktür / greater than
```

```text
False
```

```python
1 < 0 # Küçüktür / less than
```

```text
False
```

```python
0 < 1 # Küçüktür / less than
```

```text
True
```

```python
0 >= 0 # Büyüktür veya eşittir / greater than or equal to
```

```text
True
```

```python
1 >= 0 #  Büyüktür veya eşittir /greater than or equal to
```

```text
True
```

```python
-1 >= 0 #  Büyüktür veya eşittir /  greater than or equal to
```

```text
False
```

```python
0 <= 0 # Küçüktür veya Eşit değildir /less than or equal to
```

```text
True
```

```python
1 <= 0 # Küçüktür veya Eşit değildir /less than or equal to
```

```text
False
```

```python
-1 <= 0 # Küçüktür veya Eşit değildir / less than or equal to
```

```text
True
```

## Değişken \(Atama\) Operatörleri / Assignment Operators

```python
a = 1 # Değişken
```

```python
a += 1 # 1 ekle
```

```python
a -= 1 # 1 çıkar
```

```python
a *= 1 # çarp
```

```python
a /= 1 # böl
```

```python
a %= 1 # modül
```

```python
a **= 1 # üssü
```

```python
a //= 1 # Tamsayı Bölümü
```

## Veri Yapıları: Liste

```python
kelimeler = ['matematik', 'fizik', 'computer science', 'kimya'] # Liste Oluştur
```

### Üyelik Operatörleri

```python
'matematik' in kelimeler # kelimeler listesinde 'matematik' olup olmadığını kontrol eder
```

```text
True
```

```python
'matematik' not in kelimeler # kelimeler listesinde 'matematik' olmadığını kontrol eder
```

```text
False
```

### Liste Elemanlarına Erişim

```python
print('kelimeler[0]:', kelimeler[0]) # Listedeki ilk eleman
```

```text
kelimeler[0]: matematik
```

```python
print('kelimeler[-1]', kelimeler[-1]) # Listedeki son eleman
```

```text
kelimeler[-1] kimya
```

### Liste Elemanlarını Güncellemek

```python
kelimeler[0] = 'Matematik'
```

### Listenin Uzunluğu

```python
len(kelimeler)
```

```text
4
```

### Dilimleme

```python
kelimeler[1:] # sadece 2. elamandan başlayarak bütün elemanları listele
```

```text
['fizik', 'computer science', 'kimya']
```

```python
subjects[1:3] # Sadece 2. ve 3. elemanı listele
```

```text
['physics', 'computer science']
```

### Eklemek

```python
kelimeler.append('istatistik') # Yeni Eleman Eklemek
```

## Veri Yapıları: Sözlük

```python
yazılımcı = {'İsim': 'Enis Getmez', 'Alanı': 'Python'}
```

```python
print('İsim:', yazılımcı['İsim']) # sözlük değerine erişme
```

```text
İsim: Enis Getmez
```

```python
yazılımcı['Alanı'] = 'Python, C#, Java' # Sözlük değerini güncellemek
```

```python
len(yazılımcı) # Sözlük uzunluğu
```

```text
2
```

```python
yazılımcı.keys() # Başlıklara erişmek
```

```text
dict_keys(['İsim', 'Alanı'])
```

```python
yazılımcı.values() # Değerlere Erişmek
```

```text
dict_values(['Enis Getmez', 'Python, C#, Java'])
```

## Durum İfadeleri

```python
if 'Matematik' in kelimeler:
    print('Kelimeler İçerisinde Matematik var!')
```

```text
Kelimeler İçerisinde Matematik var!
```

```python
if 'matematik' in kelimeler:
    print('Kelimeler İçerisinde matematik var!')
else:
    print('Kelimeler İçerisinde matematik yok!')
```

```text
Kelimeler İçerisinde Matematik yok!
```

```python
if 'matematik' in kelimeler:
    print('Kelimeler İçerisinde matematik var!')
elif 'Matematik' in kelimeler:
    print('Kelimeler İçerisinde Matematik var!')
else:
    print('Bulunamadı')
```

```text
Kelimeler İçerisinde Matematik var!
```

## Döngü İfadeleri

```python
deger = 0

while True:
    print('Selam!', end=' ')
    if deger == 3:
        break
    else:
        deger += 1
```

```text
Selam! Selam! Selam! Selam! 
```

## Fonksiyonlar

```python
def yazi(ifade):
    print('*======*')
    print(ifade)
    print('*======*')
```

```python
yazi('Hello, World!!')
```

```text
*======*
Hello, World!!
*======*
```

```python
def add(x, y):
    return x + y
```

```python
c = add(1, 2)
print(c)
```

```text
3
```


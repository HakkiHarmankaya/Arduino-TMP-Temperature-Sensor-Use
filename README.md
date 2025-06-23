# 🌡️ Arduino #9: TMP36 Isı Sensörü ile Sıcaklık Kontrollü LED Sistemi

Bu projede, **TMP36 sıcaklık sensörü** kullanarak ortam sıcaklığına bağlı olarak **2 LED’i kontrol etmeyi** öğreneceksiniz.

🔗 [Web Siteme Bakmak İçin Tıkla](https://www.hakkiharmankaya.com/)  
🔗 [Tinkercad Tasarımına Göz At](https://www.tinkercad.com/things/5OgRetgUPne?sharecode=zlMN2AUuv66qxbJFHyT24GxijFhmqlyKFCmQkM2l1mg)

---

## 🧰 Gerekli Malzemeler

- 1 adet **TMP36 sıcaklık sensörü**
- 2 adet **LED** (farklı renklerde)
- 2 adet **direnç** (220Ω veya 330Ω)
- 1 adet **Arduino**
- 1 adet **breadboard**
- **Jumper kabloları**

---

## ⚙️ Adım Adım Devre Kurulumu

### 🔹 Adım 1: Devreyi Kurun

- TMP36:
  - **VCC pini** → **5V**
  - **GND pini** → **GND**
  - **VOUT pini** → **A0**

- LED 1 (soğuk ortam için):
  - **Anot (uzun bacak)** → **D5**
  - **Katot** → **direnç** → **GND**

- LED 2 (sıcak ortam için):
  - **Anot** → **D3**
  - **Katot** → **direnç** → **GND**

---

## 🔹 Adım 2: Arduino Kodunu Yazın ve Yükleyin

```cpp
float a;

void setup() {
  pinMode(A0, INPUT);
  pinMode(5, OUTPUT);
  pinMode(3, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  a = analogRead(A0);
  a = -40 + (a - 20) / 2.05;  // TMP36 için yaklaşık sıcaklık hesaplama

  Serial.print("Sicaklik = ");
  Serial.println(a);

  if (a <= 35)
    digitalWrite(5, HIGH);  // Soğuk: LED1 yanar
  else
    digitalWrite(5, LOW);

  if (a > 35)
    digitalWrite(3, HIGH);  // Sıcak: LED2 yanar
  else
    digitalWrite(3, LOW);
}

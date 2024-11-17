## Minikube ile Istio Kurulumuna Giriş

## Gereksinimler

Bu demo için makinenize **Minikube** kurulmuş olmalıdır. Başlangıç olarak, Minikube üzerinde bir cluster oluşturmanız gerekecek. 

## 1. Minikube ile Cluster Oluşturma
- **Default Driver**: Minikube, `start` komutuyla default driveR kullanır.

```bash
minikube start
```

## 2. Docker Driver Kullanımı ve Sorunlar

Minikube, sisteminizde **Docker** çalışıyorsa, default olarak Docker'ı bir konteyner içinde çalıştırır.

### Olası Hata:

```text
"Due to the networking limitations of driver docker darwin, ingress addon is not supported."
```

Bu hata, özellikle macOS üzerindeki Docker Bridge sınırlamalarından kaynaklanmaktadır.

### Çözüm: VM Tabanlı Driver  Kullanımı

Docker yerine **VM tabanlı bir driver** kullanarak Minikube clusterınızı oluşturun:

```bash
minikube delete
minikube start --vm=true
```

## 3. Istioctl Kurulumu

### 1. Ingress Eklentisini Etkinleştirme

Ingress eklentisini etkinleştirin ve doğrulayın: 

```bash
minikube addons enable ingress
```

### 2. Istioctl Yükleme

Sonrasında, Istioctl'yi yüklemek için aşağıdaki komutu çalıştırın:

```bash
curl -L https://istio.io/downloadIstio | sh -
```

Bu komut, mevcut dizine en son Istio sürümünü indirir.

## 4. Istio Paketinin Yapısı

İndirilen paket dizinine gidin. 

```bash
cd istio-1.**.*
```

Paket aşağıdaki önemli bileşenleri içerir:

- **samples**: Eğitim boyunca kullanılacak örnek uygulamalar.
- **tools**: Ek araçlar ve komutlar.
- **bin**: istioctl, bin klasörü içinde bulunur.

---

İstemciyi Sistem Yoluna Eklemek için:

```bash
export PATH=$PWD/bin:$PATH
```

## 5. Istioctl Kurulumunu Doğrulama

Kurulumun başarılı olduğunu doğrulamak için aşağıdaki komutu çalıştırın:

```bash
istioctl version
```

Bu komut, yüklü sürümü gösterecektir.

## 6. Istio'nun Clusterda Kurulu Olduğunu Kontrol Etmek

```bash
istioctl verify-install
```

Eğer **the server could not find the requested resource** hatasını görürseniz, control plane kurmanız gerekecektir.
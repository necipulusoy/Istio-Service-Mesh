## Deploying Our First Application on Istio

Istio'yu denemek için örnek bir uygulama deploy edeceğiz. İndirilen **samples** klasöründe **booking** uygulamasını bulabilirsiniz.

## 1. Uygulama Deploy Komutu

Aşağıdaki komutu kullanarak uygulamayı deploy edin:

```bash
kubectl apply -f samples/bookinfo/platform/kube/bookinfo.yaml
```

Bu komut, product page, details, ratings ve 3 farklı review servisi dahil olmak üzere mikroservisleri içerir.

![servis-mesh](../images/image-4.png)

## 2. Podların Durumunu Kontrol Etme

Application deploy edildikten sonra pod'ların durumunu kontrol etmek için aşağıdaki komutu çalıştırın:

```bash
kubectl get pods -A
```
Bu podların hepsi default namespace'de yer almaktadır.

![servis-mesh](../images/image-5.png)

Biz Istıo'yu install ettik. Doğal olarak her pod'un içinde ayrıca **proxy container**'ın da olmasını bekliyorduk ama pod'ların içinde sadece bir container var. Peki neden?

## 3. Istio Injection Hatası

Bu sorunun nedenini analiz etmek için aşağıdaki komutu çalıştırabilirsiniz:

```bash
istioctl analyze
```

Bu komutu çalıştıdığınızda, Istio injection özelliğinin etkin olmadığını belirten bir mesaj göreceksiniz. Peki bu mesaj ne anlama geliyor?

Clusterımıza bir çok namespace bulunmaktadır. Bizim uygulamamız şu an **default** namespace'de deploy edildi. Ama başka bir uygulama da **hr** namespace'inde deploy edilmiş olabilir. Istio sidecar özelliğini enable etmek istiyorsan mutlaka namespace seviyesinde bunu belirtmen gerekir.

![servis-mesh](../images/image-6.png)

## 4. Sidecar Injection Enable Etme

### 1. Namespace Etiketleme

Default namespace'de Istio injection özelliğini etkinleştirmek için aşağıdaki komutu kullanın:

```bash
kubectl label namespace default istio-injection=enabled
```

Bu komut ile default namespace'de oluşan podlarda otomatik olarak sidecar container oluşacak.

Eğer bu özelliği devre dışı bırakmak isterseniz, aynı komutu şu şekilde kullanabilirsiniz:

```bash
kubectl label namespace default istio-injection=disabled
```

### 2. Yeniden Deploy Etme

Label işlemi tamamlandıktan sonra, mevcut deploymentı silip yeniden deploy etmeniz gerekecek:

```bash
kubectl delete -f samples/bookinfo/platform/kube/bookinfo.yaml

kubectl apply -f samples/bookinfo/platform/kube/bookinfo.yaml
```

### 3. Sidecar Injectionı Kontrol Etme

Pod'ların durumu ve Envoy sidecar proxy'lerinin başarıyla eklendiğini kontrol etmek için:

```bash
kubectl get pods
```

![servis-mesh](../images/image-7.png)

Artık tüm pod'larda sidecar proxy'leri başarıyla eklendi.
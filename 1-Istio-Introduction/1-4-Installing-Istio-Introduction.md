## Istio Kurulumu için Yaklaşımlar

Istio'yu bir Kubernetes clusterına kurmak için üç farklı yöntem kullanabilirsiniz:
1. **istioctl** komut satırı aracı
2. **Istio Operator**
3. **Helm Paketi**

Bu eğitimde, **istioctl** aracı kullanılarak kurulum yapılacaktır.

---

## Istioctl ile Kurulum

### 1. Komut Çalıştırma
Istio'yu **istioctl** kullanarak kurmak için aşağıdaki komutu çalıştırın:

```bash
istioctl install --set profile=demo
```

## Demo Profili

- **Demo Profili**: Bu kurulum için demo profili kullanılacak.
- **Diğer Profiller**: Production ve performans testi için özel profiller bulunmaktadır. Farklı environmentların farklı profillere ihtiyacı vardır.

---

## 2. Kurulumun Yapılandırılması

Komut çalıştırıldığında, Istio clustera aşağıdaki şekilde yüklenir:

- **Deployment**: `istiod` adlı bir deployment oluşturulur.
- **Namespace**: Istio, `istio-system` namespace'inde çalışır.

---

## Istio Bileşenleri

Kurulum sırasında aşağıdaki bileşenler yüklenir:

- **Istiod**: Citadel, Pilot ve Galley gibi bileşenleri içerir.
- **Gatewayler**:
  - `istio-egressgateway`
  - `istio-ingressgateway`

Ayrıca, bu gateway'ler ve diğer bileşenler için bir dizi Kubernetes servis objesi oluşturulur. Gateway'ler hakkında daha fazla bilgi ilerleyen bölümlerde verilecektir.

---

## Kurulumu Doğrulama

Kurulum tamamlandıktan sonra aşağıdaki komutla doğrulama yapabilirsiniz:

```bash
istioctl verify-install
```

Bu komut, kurulumun başarılı olup olmadığını kontrol eder ve yüklenen tüm bileşenlerin listesini gösterir.

---

##  Kubernetes ile Entegrasyon

Istio, Kubernetes'i genişletir ve Custom Resource Definitions (CRD) kullanır. Bu kaynakları doğrulamak ve çalışmasını izlemek için CRD'lere göz atabilirsiniz.

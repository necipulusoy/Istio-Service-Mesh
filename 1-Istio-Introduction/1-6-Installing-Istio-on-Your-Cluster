## Demo: Istioctl ile Istio Kurulumu

Bu demoda, clustera **Istioctl** kullanarak Istio'yu kuracağız. Demo amacıyla, **demo profili** kullanacağız.

### 1. Istio'yu Kurma

Aşağıdaki komutla Istio'yu kurun:

```bash
istioctl install --set profile=demo -y
```

### 2. Kurulumu Doğrulama

Kurulum tamamlandıktan sonra, her şeyin doğru bir şekilde yüklendiğinden emin olmak için aşağıdaki komutu çalıştırın:

```bash
istioctl verify-install
```

Bu komut, kurulumda herhangi bir sorun olup olmadığını kontrol eder.

### 2. Yeni Resource

Kurulumdan sonra clusterınızda birçok yeni resource eklenecektir. Bu resourcelardan bazıları şunlardır:

- **Cluster Roles** ve **Cluster Role Bindings**
- **Custom Resource Definitions (CRDs)**
- **3 Istio Deployments** (13 custom definition ile)



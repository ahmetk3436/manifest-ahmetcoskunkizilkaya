# Manifest-ahmetcoskunkizilkaya Kurulum ve Yapılandırma

## Giriş

Bu klasör, Kubernetes manifest'lerini Kustomize kullanarak yönetmek için gerekli dosyaları içerir. Base ve overlays (dev, prod) ile ortam bazlı konfigürasyonlar sağlanır.

## Gereksinimler

- Çalışan bir Kubernetes kümesi
- kubectl kurulu
- Kustomize kurulu (kubectl ile entegre edilebilir)

## Dosyalar

- `base/`:
  - `deployment.yaml`: Uygulama deployment'ı
  - `kustomization.yaml`: Base kustomization
  - `service.yaml`: Service tanımı
- `overlays/dev/`:
  - `configmap.yaml`: Dev ortam ConfigMap
  - `kustomization.yaml`: Dev kustomization
- `overlays/prod/`:
  - `configmap.yaml`: Prod ortam ConfigMap
  - `kustomization.yaml`: Prod kustomization

## Kurulum Adımları

1. **Hazırlık:**
   - Kubernetes kümenizin çalıştığından emin olun.

2. **Dev Ortamı Deploy Edin:**
   ```bash
   cd /root/infra-ahmetcoskunkizilkaya/manifest-ahmetcoskunkizilkaya
   kubectl apply -k overlays/dev
   ```

3. **Prod Ortamı Deploy Edin:**
   ```bash
   kubectl apply -k overlays/prod
   ```

4. **Doğrulama:**
   - Deployment'ları kontrol edin:
     ```bash
     kubectl get deployments
     ```
   - Service'leri kontrol edin:
     ```bash
     kubectl get services
     ```

## Erişim

- Uygulama service üzerinden erişilebilir (service.yaml'de tanımlı portlar).

## Özelleştirme

- ConfigMap'leri overlays içindeki yaml dosyalarında düzenleyin.
- Deployment spec'ini base/deployment.yaml'de değiştirin.

## Sorun Giderme

- Apply hataları: `kubectl describe` ile detay alın.
- Kustomize sorunları: `kubectl kustomize overlays/dev` ile önizleme yapın.

Bu setup, farklı ortamlar için modüler manifest yönetimi sağlar.
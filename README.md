
# Flask Hello World App
Bu proje, basit bir Flask web uygulaması içerir ve konteynerize edilmiştir. Uygulama Kubernetes üzerinde dağıtım yapmak üzere yapılandırılmıştır.

## İçindekiler
app.py: Flask uygulaması için kaynak kodu.

Dockerfile: Docker imajı oluşturmak için kullanılan tanım dosyası.

deployment.yaml: Kubernetes deployment tanım dosyası.

service.yaml: Kubernetes service tanım dosyası.

requirements.txt: Gerekli bileşenler için source

## Gereklilikler
Docker Desktop
Kubernetes

## Kurulum

### Docker

1-Projeyi bilgisayarınıza klonlayın ve terminalde klonladığınız dizine gidin.

```
git clone https://github.com/astavist/WEEK3.git

cd <repository_directory>
```

2-Projenin bulunduğu dizindeki Dockerfile ile bir Docker imajı oluşturun.

```
docker build -t hello-world-flask .
```

3- Oluşturulan Docker imajını kullanarak bir container çalıştırın.

```
docker run -p 5000:5000 hello-world-flask
```

4- Proje DockerHub üzerinde astavist/hello-world-flask imajını kullanıyor. Eğer bu imajı değil de kendi imajınızı kullanmak isterseniz:
```
docker tag hello-world-flask <yourusername>/hello-world-flask
docker push <yourusername>/hello-world-flask
```
ve deployment.yaml dosyasındaki "spec:template:spec:containers:image: astavist/hello-world-flask" kısmını güncellemeniz gerekiyor.



Bu aşamada artık http://localhost:5000 e bağlandığınızda ekranınızda Hello World! yazması gerekiyor.

### Kubernetes

1- Klonladığınız proje içerisinde deployment ve service yaml tanım dosyaları mevcut. Bu dosyalar aracılığıyla dağıtım yapabilirsiniz.

```
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

2-Dağıtımı kontrol etmek için
```
kubectl get services
```
### Scaling
Terminalde aşağıdaki kod parçacıklarını kullanarak scale edebilirsiniz.
```
kubectl get deployments
```
Bu ilk kodda deployment'ımızın adını buluyoruz

```
kubectl scale deployment hello-world-deployment --replicas=3
```
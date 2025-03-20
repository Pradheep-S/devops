# Installing and setting up Kubernetes Minikube

## Update system packages and Install dependencies

```bash
mkdir docker
nano  Dockerfile
npm init -y
npm init -y // again if the previous command installed npm
cd ..
docker pull pradheep255/docker-test:latest . // replace with your docker uid/repo:image_tag
cd docker
docker build -t pradheep255/docker-test/latest
```
![Screenshot from 2025-03-20 14-51-15](https://github.com/user-attachments/assets/a5ad69b0-f01c-4c48-bd11-aa5741044d42)
```bash
docker ps -a
sudo nano nginx-deployment.yaml
kubectl apply -f nginx-deployment.yaml
sudo nano service.yaml
kubectl apply -f service.yaml
kubectl get pods
minikube get svc my-app
minikube service my-app --url
```
![Screenshot from 2025-03-20 15-55-02](https://github.com/user-attachments/assets/4064e81c-505d-4ec8-a723-5df241e70715)
![Screenshot from 2025-03-20 14-51-28](https://github.com/user-attachments/assets/25c6a967-03da-4ba9-8562-cdfb45e3256d)
```bash
minikube tunnel
```
![Screenshot from 2025-03-20 14-52-06](https://github.com/user-attachments/assets/37cf98a2-f0a8-4eab-a8f9-8a5d464076c4)
 - open the url in browser
```bash
curl <url>
```
![Screenshot from 2025-03-20 15-56-12](https://github.com/user-attachments/assets/36a19b32-95a8-4df0-b49d-62a8444b5fa8)

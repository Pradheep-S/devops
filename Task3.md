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
## Install Docker, Kubectl and Minikube
### Install Docker
```bash
sudo apt install -y docker.io
sudo systemctl start docker
sudo systemctl enable docker
docker --version
```
### Install Kubectl
```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
kubectl version --client
```
### Install Minikube
```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
minikube version
```

![Screenshot from 2025-03-20 14-51-15](https://github.com/user-attachments/assets/a5ad69b0-f01c-4c48-bd11-aa5741044d42)

### Fix Docker setup
```bash
sudo usermod -aG docker $USER
reboot
```

### Verify Installation after reboot
```bash
docker run hello-world
```
### Start and open Minikube
```bash
minikube start --driver=docker
minikube dashboard
```
![Screenshot from 2025-03-21 10-06-42](https://github.com/user-attachments/assets/a7e17f08-0317-47cb-b171-dc2cb263e2f7)
 - Go to `my-app`

![Screenshot from 2025-03-21 10-06-26](https://github.com/user-attachments/assets/c506430f-b607-4d2a-b95e-83fe1bc16427)

- Configure the yaml files
  
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
### Config file codes
Dockerfile
```groovy
# Use an official Node.js runtime as a base image
FROM node:18

# Set the working directory
WORKDIR /app

# Copy package.json and install dependencies
COPY package.json ./
RUN npm install

# Copy the rest of the application
COPY . .

# Expose port 3000 and start the app
EXPOSE 3000
CMD ["npm", "start"]
```

nginx-deployment.yaml
```groovy
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-app
        image: pradheep255/docker-test:latest
        imagePullPolicy: IfNotPresent
        ports:
        - containerPort: 8080
```

service.yaml
```groovy
apiVersion: v1
kind: Service
metadata:
  name: my-app
  namespace: default
spec:
  type: NodePort  # Ensures external access via a specific port
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80       # Service port inside the cluster
      targetPort: 80  # The container's port
      nodePort: 30391   # Externally accessible port
```
![Screenshot from 2025-03-20 14-51-28](https://github.com/user-attachments/assets/25c6a967-03da-4ba9-8562-cdfb45e3256d)

- Check the available Kubernetes services in your local machine
```bash
minikube tunnel
```
![Screenshot from 2025-03-20 14-52-06](https://github.com/user-attachments/assets/37cf98a2-f0a8-4eab-a8f9-8a5d464076c4)
```bash
minikube service my-app --url
```
 - open the url in browser
```bash
curl <url>
```
![Screenshot from 2025-03-20 15-56-12](https://github.com/user-attachments/assets/36a19b32-95a8-4df0-b49d-62a8444b5fa8)

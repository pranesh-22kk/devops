# Installing and Setting Up Kubernetes Minikube


```bash
mkdir my-docker-app
```
```bash
cd my-docker-app
```
```bash
touch Dockerfile
```
```bash
apt install npm
```
```bash
npm init -y
```
```bash
docker pull pranesh22/pro:latest
```
```bash
docker build -t pranesh22/pro:latest
```
```bash
docker ps
```
```bash
cd ..
```
```bash
minikube start
```
```bash
sudo nano nginx-deploymenr.yaml
```

## nginx-deploymenr.yaml

```bash
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
        image: pranesh22/pro:latest
        imagePullPolicy: IfNotPresent
        ports:
        - containerPort: 80
```

```bash
sudo nano service.yaml
```

## service.yaml

```bash
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
      targetPort: 8080  # The container's port
      nodePort: 30391   # Externally accessible port
```

```bash
kubectl apply -f nginx-deploymenr.yaml
```
```bash
kubectl apply -f service.yaml
```
```bash
kubectl get pods
```
```bash
kubectl get svc my-app
```
```bash
minikube service my-app --url
```
```bash
curl <url>
```

![Screenshot from 2025-03-20 06-53-33](https://github.com/user-attachments/assets/46505648-95a6-4fcc-b37e-1a852617947b)
![Screenshot from 2025-03-20 06-54-17](https://github.com/user-attachments/assets/38524f3d-8792-4968-b2e2-68f027757674)
![Screenshot from 2025-03-20 06-54-47](https://github.com/user-attachments/assets/ebea421f-0914-4be0-8917-d611f63b9e13)
![Screenshot from 2025-03-20 06-54-25](https://github.com/user-attachments/assets/1b8a497a-a9cd-4c16-9720-7cb7c8eec2a2)
![Screenshot from 2025-03-20 00-48-06](https://github.com/user-attachments/assets/933e91fb-a325-44c0-92a1-2e889290bb30)


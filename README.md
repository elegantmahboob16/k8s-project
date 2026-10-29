# Kubernetes Car Game (Traffic Dodger)

A small browser game served by Nginx and deployed on Kubernetes.

## Tech stack
Docker, Docker Hub, Kubernetes (kind), Nginx, AWS EC2

## How it works
1. `dockerfile` puts `index.html` into the `nginx:alpine` image
2. The image is pushed to Docker Hub
3. `deployment.yaml` runs 2 replicas (pods) of the image
4. `service.yaml` exposes the pods with a NodePort Service

## Run it
docker build -t YOUR_DOCKERHUB_USERNAME/car-game:v1 -f dockerfile .
docker push YOUR_DOCKERHUB_USERNAME/car-game:v1
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl port-forward --address 0.0.0.0 service/car-game-service 8080:80

Open http://SERVER-IP:8080 and use the left and right arrow keys.

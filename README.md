docker login
docker pull frontend and backend images
kubectl apply -f ./k8/fullstack-deployment.yml





# 1. Delete the old namespace

kubectl delete namespace fullstack-app

# 2. Build and push new Docker images (If code is modified)

cd reactfrontend
docker build -f frontend.Dockerfile -t username/k8-frontend:latest .
docker push username/k8-frontend:latest

cd springbootbackend
docker build -f backend.Dockerfile -t username/k8-backend:latest .
docker push username/k8-backend:latest

# 3. Reapply deployment configuration

kubectl apply -f ./k8/fullstack-deployment.yml

# 4. Check that everything is up and running

kubectl get all -n fullstack-app


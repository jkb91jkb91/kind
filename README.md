
# START KIND with 1 master + 2 workers
kind create cluster --name ing --config ingress-config.yaml

# How to ssh to worker
docker exec -it WORKER_NAME bash

# How to list kind clusters
kind get clusters

# How to delete clusters
kind delete cluster --name ing


# SERVICES APPLY
kubectl apply -f ingress.yaml && kubectl apply -f deployment.yaml && kubectl apply -f service.yaml

# INSTALL INGRESS
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml
kubectl wait --namespace ingress-nginx --for=condition=ready pod --selector=app.kubernetes.io/component=controller --timeout=90s

# SERVICE APPLY INGRESS
kubectl apply -f ingress.yaml


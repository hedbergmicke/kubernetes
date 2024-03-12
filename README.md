# kubernetes
### Bygga en enkel app

**ConfigMap**\
mongo-config.yml Skapa en ConfigMap för kopplin till databas\
data: mongo-url: mongo-service (namn på service)

**Secret**\
mongo-secret.yml Skapa en secret för db och webb

**Deployment**\
mongo.yml Skapa en deployment för databasen
image: mongo:5.0\
user and pass under dockerhub

        env:
        - name: USER_NAME
          valueFrom:
            secretKeyRef:
              name: mongo-secret
              key: mongo-user
        - name: USER_PWD
        - name: DB_URL
          valueFrom:
            configMapKeyRef:
              name: mongo-config
              key: mongo-url

containerPort: 27017

web-app.yml Skapa en deployment för databasen
image: nanajanashia/k8s-demo-app:v1.0\
containerPort: 3000

**Service**\
Skapa en service för mongo
mongo.yml
selector: Selects the pods to forward the requests to

Skapa en service för webbapp
web-app.yml
selector: Selects the pods to forward the requests to
spec: type: NodePort


# Testa
* kubectl get all
* kubectl get configmap
* kubectl get secret
* kubectl describe ...
* kubectl get service (för att se port)
* kubectl get node -o wide (för att se nodens ip)
* kubectl exec -it <pod_name> -- env
* nc -zv 10.42.1.22 3000 (check port)

# Mer att utvärdera
* volumes
* ingres privat ip
* secretshantering
* gethub

# MetalLB
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.10.3/manifests/namespace.yaml
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.10.3/manifests/metallb.yaml

## Simple nginx deployment med LoadBalancer (extern ip)
kubectl create deploy nginx --image=nginx
kubectl expose deploy nginx --port=80 --target-port=80 --type=LoadBalancer
kubectl get svc nginx


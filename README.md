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
containerPort: 27017

**Service**\
Skapa en service för mongo
mongo.yml



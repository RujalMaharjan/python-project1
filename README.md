
# Python API Server
This is a simple Python API Server that is deployed from Docker Hub. It sends data using POST requests to save data to MongoDB.

## Prerequisites
Before you begin, ensure you have met the following requirements:

- Docker is installed.
- MongoDB Compass is installed to verify if data is sent to the MongoDB container.


## Creating a Docker Network
Create a Docker network to facilitate communication between your Python application container and a MongoDB container.

Replace <network-name> with a name of your choice:

```bash
docker network create <network-name>
```

## Run MongoDB Container
Pull a MongoDB image from Docker Hub and run it within the Docker network you created. Ensure that it's named mongodb so that it matches the connection string in your modified Python application

Replace <network-name> with the name of network you created earlier
```bash
docker run --network <network-name> --name mongodb -d -p 27017:27017 -v my_mongo_data:/data/db mongo:latest
```

## Run Your Python Application Container
Run your Docker image as a container within the same Docker network. Ensure it can successfully communicate with the MongoDB container

Replace <network-name> with the name of network you created earlier
```bash
docker run --network < network-name> -d -p 3000:3000 --name project rujalmhn/python-project1:V1.0
```


## Sending data to MONGODB
To interact with the application, you can use the following command to create a new item in the database:
- To use 'curl' command in windows you can use postman to send the data.

## For macOS and Linux:
```bash
curl -X POST http://localhost:3000/items \
     -H "Content-Type: application/json" \
     -d '{"id": "4", "name": "maziar"}'
```
## For Windows:
```bash
Invoke-RestMethod -Uri http://localhost:3000/items -Method Post -ContentType "application/json" -Body '{"id": "4", "name": "maziar"}'
```


## Check for Data in MongoDB Compass
- Open MongoDb Compass and click connect
- In the left panel, click mydb, and within mydb, click items.
- You should see the data that we sent to MongoDB here.
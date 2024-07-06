
# Python API Server

This is a simple Python API Server using POST to save data to MongoDB and GET requests to receive the data from MongoDB.

## Prerequisites

Before you begin, ensure you have met the following requirements:

- You have installed Docker
- You have  installed postman and mongodb compass to check if the created containers can send data to the created mongodb database container


## Creating a Docker Network

Create a Docker network to facilitate communication between your Python application container and a MongoDB container.
```bash
docker network create < network-name >
```

## Run MongoDB Container

Pull a MongoDB image from Docker Hub and run it within the Docker network you created. Ensure that it's named mongodb so that it matches the connection string in your modified Python application
```bash
docker run --name mongodb --network < network-name > -d -p 27017:27017 -v my_mongo_data:/data/db mongo:latest
```

## Run Your Python Application Container
Run your Docker image as a container within the same Docker network. Ensure it can successfully communicate with the MongoDB container
```bash
docker run --network < network-name > -d -p 3000:3000 --name project rujalmhn/python-project1:V1.0
```


## Using the Application

To interact with the application, you can use the following `curl` command to create a new item in the database:
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

## Contributing to the Project

Contributions to enhance the project are welcome. Please fork the repository and create a pull request.

## License

This project is licensed under the GPLv3.

---


Docker Compose - Run multiple Docker containers
Technologies used:

- Docker, MongoDB, MongoExpress

Project Description:

1. Write Docker Compose file to run MongoDB and MongoExpress containers

-------------------------------------------------------------------------------

1. create a new yaml file


```yaml
version: '3'
services:
  # my-app:
    # image: ${docker-registry}/my-app:1.0
    # ports:
     # - 3000:3000
  mongodb:
    image: mongo
    ports:
     - 27017:27017
    environment:
     - MONGO_INITDB_ROOT_USERNAME=admin
     - MONGO_INITDB_ROOT_PASSWORD=password
    volumes:
     - mongo-data:/data/db
  mongo-express:
    image: mongo-express
    # To make sure Mongo express can connect to MongoDB container, when we start, this is down to the possibility that Mongo
    # express starts first, and will need to wait till the DB is up
    restart: always
    ports:
     - 8081:8081
    environment:
     - ME_CONFIG_MONGODB_ADMINUSERNAME=admin
     - ME_CONFIG_MONGODB_ADMINPASSWORD=password
     - ME_CONFIG_MONGODB_SERVER=mongodb
    depends_on:
     - "mongodb"
volumes:
  mongo-data:
    driver: local
```

2. Nana goes on to say, that you can use other methods like depends_on, healthcheck etc instead of the "restart policy"
3. save the file as mongo.yaml & in the js-app folder
4. run the compose file

```bash
# the -f is for file, and up tells docker what action to take
docker-compose -f mongo.yaml up
```

5. You can see during the terminal output, Mongo-Express retarted a few times while it waited to get a connection to the DB






# platform
Docker-compose file
//start of docker-compose.yml
version: '3'

services:
  mongo:
    image: mongo:3.4-windowsservercore
    container_name: mongo
    hostname: mongo

  rabbitmq:
    image: micdenny/rabbitmq-windows
    container_name: rabbit
    hostname: rabbit

  exporting:
    image: jwissink/exporting:latest
    container_name: exporting
    depends_on:
      - mongo
      - rabbitmq
      - logging
      - formatting
    

  formatting:
    image: jwissink/formatting:latest
    container_name: formatting
    depends_on:
      - mongo
      - rabbitmq
      - logging
    


  logging:
    image: jwissink/logging:latest
    container_name: logging
    depends_on:
      - mongo
      - rabbitmq
    

  webhook:
    image: jwissink/webhook:latest
    depends_on:
      - mongo
      - rabbitmq
      - logging
      - formatting
    container_name: webhook



# Python container

## 1 Create the Dockerfile

```
# Use an official Python runtime as a parent image
FROM python:3.9-slim

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Run a command that will keep the container running
# CMD tail -f /dev/null
```

## 2 Create a docker-compose file
```yml
version: '3'
services:
  myapp:
    build:
      context: .
      dockerfile: Dockerfile
    volumes:
      - ./app:/app
    command: tail -f /dev/null # to keep running the container
```

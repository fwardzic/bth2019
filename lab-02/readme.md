LAB 02 docker compose

The goal of this labs is to create a composable instruction to that will setup two-tier application (web and DB) and expose service for web server to be reachable by users.

Go to the cloned repository -> lab02 folder, create a 'dockerfile' with the instruction to do following when the image will be build:

1. use `python:3.4-alpine` image
2. create folder `code` in the root directory
3. add file `app.py` and `requirement.txt` to the /code folder inside container
4. change work dir to /code when the container will run
5. install required packages `pip install -r requirements.txt`
6. when contaner will start it should run app.py application (`python app.py`)

Once dockerfile will be created, start working on instruction to build docker image, run it and expose its service in one manifest file.

~~~version: '3'
services:
  web:
    build: .
    ports:
     - "5000:5000"
  redis:
    image: "redis:alpine"~~~
    
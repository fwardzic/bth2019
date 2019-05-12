## LAB 01 - creating container with 2048 game

In this excercise you will create container which will contain web-server with the 2048 game.

First clone git repository with the 2048 game:

`git clone https://github.com/gabrielecirulli/2048`

All credits goes to Gabriele Cirulli - author of the 2048 game.

then create "dockerfile":

`touch dockerfile`

Using PWD editor or vi in terminal, paste following content:

~~~~
FROM alpine:latest
MAINTAINER fwardzic
RUN apk --update add nginx
ADD 2048/ /usr/share/nginx/html
RUN mkdir -p /run/nginx # <- new line
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
~~~~


FROM nginx:alpine

RUN apk update
RUN apk add curl

COPY ./usr/share/nginx/html /usr/share/nginx/html
COPY ./etc/nginx/conf.d /etc/nginx/conf.d

COPY ./key /key

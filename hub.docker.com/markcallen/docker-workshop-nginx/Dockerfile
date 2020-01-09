FROM nginx

MAINTAINER Mark C Allen "mark.allen@hootsuite.com"

RUN apt-get update
RUN apt-get install -y curl

COPY public/ /usr/share/nginx/html

# FROM nginx
FROM nginx:alpine

RUN apk update


RUN apk upgrade


RUN apk add --update curl

# RUN rm /etc/nginx/sites-enabled/default
ADD sites-enabled/ /etc/nginx/sites-enabled
WORKDIR /etc/nginx/conf.d
# ADD ./default.conf /etc/nginx/conf.d/default.conf
ADD ./default.conf default.conf


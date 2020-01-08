FROM alpine 

MAINTAINER "Playa.Ru Team" <info@playa.ru> 

RUN apk update \ 
 && apk upgrade \ 
 && apk add --no-cache \ 
            rsync \ 
            openssh-client \ 
            libintl \
            gettext \
 && rm -rf /var/cache/apk/*
 

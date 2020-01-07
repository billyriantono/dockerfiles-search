FROM alpine:edge

RUN apk update  
RUN apk add gdal --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing 
RUN apk add gdal-dev --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing 
RUN apk add python3
RUN apk --update add --virtual build-dependencies  python3-dev gcc g++ 

RUN pip3 install gdal

RUN apk del build-dependencies && apk del gdal-dev

FROM node:12.12-alpine

RUN apk --no-cache update \ 
    && apk --no-cache add g++ make bash zlib-dev libpng-dev \
    &&  rm -fr /var/cache/apk/*
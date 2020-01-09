FROM ubuntu:16.04

RUN apt-get update && apt-get install -y nodejs-legacy npm nginx cntlm

RUN npm install -g grunt-cli coffee-script

RUN npm config set proxy http://127.0.0.1:3128 && \
    npm config set https-proxy http://127.0.0.1:3128

COPY ./nginx.conf /etc/nginx/nginx.conf

WORKDIR /www

CMD service cntlm stop && service cntlm start && \
    nginx -g "daemon off;"
 

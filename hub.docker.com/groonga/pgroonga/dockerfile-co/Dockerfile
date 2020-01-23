FROM node:slim 

RUN npm install -g http-proxy-to-socks

VOLUME /src
WORKDIR /src

ENV SOCKS_SERVER 127.0.0.1:1080
ENV PROXY_PORT 8000

EXPOSE 8000

CMD ["hpts -h"]

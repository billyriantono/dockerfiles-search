FROM gliderlabs/alpine:3.1
MAINTAINER Chris George <chris.a.george@gmail.com>
RUN apk --update add nodejs
RUN npm install -g private-bower
EXPOSE 5678
WORKDIR /app
ADD ./bowerConfig.json /app/bowerConfig.json
ENTRYPOINT private-bower --config /app/bowerConfig.json

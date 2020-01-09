FROM node:13.1-alpine

EXPOSE 8081
EXPOSE 8082

RUN apk update && apk upgrade && \
    apk add --no-cache bash git openssh

RUN npm -g install http-server && \
    npm install ws

WORKDIR /app
RUN git clone https://github.com/phoboslab/jsmpeg.git .

CMD ["node", "websocket-relay.js",  "stream-input",  "8081", "8082"]

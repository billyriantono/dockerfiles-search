FROM node:8-alpine

# Add dockerize dependency
RUN apk add --no-cache openssl

ENV DOCKERIZE_VERSION v0.6.1
RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && tar -C /usr/local/bin -xzvf dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && rm dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz

# Create app directory
WORKDIR /usr/src/app

COPY entrypoint.sh /
RUN chmod +x /entrypoint.sh

COPY package*.json ./

RUN npm install

# Bundle app source
COPY . .

ENTRYPOINT ["/entrypoint.sh"]

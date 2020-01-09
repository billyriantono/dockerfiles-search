FROM node:4.4-slim

MAINTAINER me@minhcd.com

# Copy app to /src
COPY . /src

# Install app and dependencies into /src
RUN cd /src && npm install

EXPOSE 8080

WORKDIR /src

ENTRYPOINT ["node", "./app.js"]

FROM node:9.5-slim

RUN apt-get update -y \
    && apt-get -y install curl python build-essential git ca-certificates 

RUN mkdir -p /app /app/bin /app/routes /app/views /app/public

RUN npm install pm2 -g

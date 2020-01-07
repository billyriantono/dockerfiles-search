FROM node:latest

RUN apt-get update \
    && apt-get install -y expect-dev \
    && rm -rf /var/lib/apt/lists/*

RUN npm install -g nsp

ARG GO_VERSION=latest
ARG PRISMA_VERSION=latest

FROM golang:$GO_VERSION

WORKDIR /app

RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - && apt-get install -y nodejs
RUN npm i -g prisma@$PRISMA_VERSION

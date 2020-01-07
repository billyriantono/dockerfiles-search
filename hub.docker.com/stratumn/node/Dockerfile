FROM node:8.9.1-alpine
# install migrate
RUN apk update
RUN apk add curl
RUN curl -L https://github.com/golang-migrate/migrate/releases/download/v4.1.0/migrate.linux-amd64.tar.gz | tar xvz
RUN mv migrate.linux-amd64 /usr/local/bin/migrate 
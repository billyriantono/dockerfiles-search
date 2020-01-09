FROM node:latest

LABEL maintainer=peter@custode.eu

RUN npm install -g ganache-cli geth

WORKDIR /usr/local/bin/

COPY docker-entrypoint.sh .

RUN chmod 777 docker-entrypoint.sh

EXPOSE 8545

ENTRYPOINT [ "docker-entrypoint.sh" ]

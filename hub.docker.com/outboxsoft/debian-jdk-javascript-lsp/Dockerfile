FROM openjdk:8-slim

RUN apt-get update

RUN apt-get install -y curl

RUN curl -sL https://deb.nodesource.com/setup_11.x | bash -
RUN apt-get install -y nodejs

RUN npm init -y

RUN npm install javascript-typescript-langserver

EXPOSE 4417

CMD [ "node", "node_modules/javascript-typescript-langserver/lib/language-server", "-p", "4417" ]
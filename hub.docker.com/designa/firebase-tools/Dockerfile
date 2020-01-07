FROM node:12.13-slim as node
LABEL maintainer "Designa <contato@designa.com.br>"

WORKDIR /app

RUN npm install -g firebase-tools

# Reference: https://github.com/jfroom/docker-compose-rails-selenium-example
COPY ./docker-entrypoint.sh /
ENTRYPOINT ["/docker-entrypoint.sh"]
RUN chmod +x /docker-entrypoint.sh

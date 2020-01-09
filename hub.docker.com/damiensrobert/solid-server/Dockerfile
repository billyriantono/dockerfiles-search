FROM node:13.0.1-stretch

EXPOSE 443

RUN npm install -g solid-server

VOLUME ["/site"]

CMD ["solid", "start", "--config-file", "/site/config.json"]

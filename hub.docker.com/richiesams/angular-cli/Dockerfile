FROM node:8.2.0-alpine

RUN npm install -g @angular/cli

COPY docker-entrypoint.sh /docker-entrypoint.sh
ENTRYPOINT ["/docker-entrypoint.sh"]

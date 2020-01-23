# Dockerfile for backend app
FROM node:12.10-stretch-slim

LABEL maintainer="Black Eye Technology"

ENV NODE_ENV=production

USER node
WORKDIR /home/node
COPY --chown=node:node package*.json ./

RUN set -e && \
  npm install --production

COPY --chown=node:node  . ./

RUN set -e && \
  npm run build

EXPOSE 8000

CMD ["./dist/main"]

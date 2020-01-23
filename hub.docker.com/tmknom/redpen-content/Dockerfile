FROM node:10.15.3-alpine as builder

ADD . /app

WORKDIR /app

RUN set -x \
  && apk --no-cache add --virtual builds-deps build-base python \
  && npm ci \
  && npm rebuild bcrypt --build-from-source \
  && npm run build \
  && npm prune --production

FROM node:10.15.3-alpine

COPY --from=builder /app/dist /app/dist
COPY --from=builder /app/node_modules /app/node_modules
COPY --from=builder /app/package.json /app/package.json

WORKDIR /app

RUN set -x && npm install -g

RUN chown -R node:node /app

USER node

ENTRYPOINT [ "govaascli" ]

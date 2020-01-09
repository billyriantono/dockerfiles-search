FROM node:12-alpine as builder

WORKDIR /usr/src/app
COPY webapp .
RUN \
  npm ci && \
  npm test && \
  npm run build

FROM node:12-alpine
WORKDIR /app
COPY server .
RUN \
  npm ci && \
  mkdir /data && \
  mkdir /public

COPY --from=builder /usr/src/public /public

EXPOSE 8080
VOLUME /data

CMD ["npm", "start"]

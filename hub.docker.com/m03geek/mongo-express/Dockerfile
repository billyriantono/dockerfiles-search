
FROM node:10-alpine as base
RUN apk add --no-cache git
RUN npm i mongo-express
WORKDIR /node_modules/mongo-express
RUN npm i
RUN cp config.default.js config.js

FROM mhart/alpine-node:base-10
ENV NODE_ENV="production" \
    ME_CONFIG_EDITORTHEME="default" \
    ME_CONFIG_MONGODB_SERVER="mongo" \
    ME_CONFIG_MONGODB_ENABLE_ADMIN="true" \
    ME_CONFIG_BASICAUTH_USERNAME="" \
    ME_CONFIG_BASICAUTH_PASSWORD="" \
    VCAP_APP_HOST="0.0.0.0"
COPY --from=base /node_modules/mongo-express /app
RUN apk add -u --no-cache tini
WORKDIR /app
EXPOSE 8081
ENTRYPOINT ["/sbin/tini", "--"]
CMD ["node",  "app.js"]

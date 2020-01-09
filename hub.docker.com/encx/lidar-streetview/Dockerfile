FROM node:12-alpine as apiBuilder
WORKDIR /api
COPY api/package.json api/yarn.lock ./
RUN yarn
COPY api .
RUN yarn prestart

FROM node:12-alpine as clientBuilder
WORKDIR /client
COPY client/package.json client/yarn.lock ./
RUN yarn
COPY client .
RUN yarn build

FROM node:12-alpine AS final
EXPOSE 8000
COPY --from=apiBuilder /api/package.json /api/yarn.lock /app/api/
COPY --from=apiBuilder /api/dist /app/api/dist
COPY --from=clientBuilder /client/dist/ /app/_client/
COPY docker-resources/startup.sh /app/api/
RUN ["chmod", "+x", "/app/api/startup.sh"]
WORKDIR /app/api
RUN yarn install --production

ENTRYPOINT ["/app/api/startup.sh"]
FROM node:12-alpine as base

WORKDIR /app

CMD yarn install && yarn start

FROM base as build

COPY src .

RUN yarn install --production \
  && yarn build

FROM nginx:1.17-alpine as prod

COPY --from=build /app/build /usr/share/nginx/html

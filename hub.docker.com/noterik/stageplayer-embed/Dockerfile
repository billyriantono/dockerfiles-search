FROM node:alpine as builder

RUN mkdir /app && chown node:node /app

WORKDIR /tmp
COPY app/package.json app/yarn.lock /tmp/
RUN yarn install --pure-lockfile
WORKDIR /app
COPY ./app /app/
RUN cp -a /tmp/node_modules /app
RUN yarn build

FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html/
EXPOSE 80
FROM node:8.16.0 AS build-env
WORKDIR /app

RUN npm -g config set user root
RUN npm install -g elm

COPY src/ ./src/
COPY elm.json .
RUN elm make ./src/Main.elm --output=app/index.html

FROM nginx:alpine
WORKDIR /app
COPY default.conf /etc/nginx/conf.d/default.conf
COPY --from=build-env ./app/app/index.html /usr/share/nginx/html/index.html
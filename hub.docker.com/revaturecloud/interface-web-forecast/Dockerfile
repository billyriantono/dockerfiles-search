# STAGE - BUILD
FROM node:8-alpine as build
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm ci
COPY . ./
RUN npm run build-lib
RUN npm run build

# STAGE - DEPLOY
FROM nginx:1.14-alpine as deploy
RUN rm -rf /usr/share/nginx/html/*
COPY nginx-custom.conf /etc/nginx/conf.d/default.conf
ARG APP_NAME=interface-web-forecast
COPY --from=build /app/dist/${APP_NAME} /usr/share/nginx/html/

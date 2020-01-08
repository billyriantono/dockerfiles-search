# Build Stage
FROM node:lts-alpine as build-stage

WORKDIR /app

COPY ./package*.json ./

RUN npm install

COPY . .

RUN $(npm bin)/ng build --prod

# Compiled App Stage
FROM nginx:alpine

COPY --from=build-stage /app/dist/admin-platform/ /usr/share/nginx/html

COPY ./nginx.conf /etc/nginx/conf.d/default.conf

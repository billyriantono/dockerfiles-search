FROM node:8.11.2-alpine as node

WORKDIR /usr/src/app

COPY ./frontend/package*.json ./

RUN npm install

COPY ./frontend/. .

RUN npm run build 

# Stage 2
FROM nginx:1.13.12-alpine

COPY --from=node /usr/src/app/dist /usr/share/nginx/html

COPY ./server/nginx.conf /etc/nginx/conf.d/default.conf
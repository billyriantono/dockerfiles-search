FROM node:8.4 AS build-env
COPY . /app
WORKDIR /app
RUN npm install
RUN npm run build

FROM nginx:1.13-alpine
COPY --from=build-env /app/public /var/www/public
COPY nginx.conf /etc/nginx/nginx.conf
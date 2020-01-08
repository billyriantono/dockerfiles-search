# Build Stage
FROM node:9.11.1-alpine as build-stage
WORKDIR /app
COPY .npmrc .npmrc
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Production Stage
FROM nginx:1.13.12-alpine
COPY ./docker/nginx/conf.d /etc/nginx/conf.d
COPY ./docker/nginx/conf/nginx.conf /etc/nginx/conf/nginx.conf
COPY --from=build-stage /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
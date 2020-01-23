# build environment
FROM node:10-alpine as node
ENV PATH /app/node_modules/.bin:$PATH
RUN mkdir /app
WORKDIR /app
RUN npm install -g @angular/cli@7.0.2

FROM nginx:1.13
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80

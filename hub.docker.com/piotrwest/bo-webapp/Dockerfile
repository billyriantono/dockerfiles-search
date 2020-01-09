#This builds webapp prod image - distribution package served by NGINX
FROM node:latest as builder
WORKDIR /usr/src/app
COPY package.json /usr/src/app/package.json
RUN npm install
COPY . /usr/src/app
RUN npm run build:prod

FROM nginx:alpine
COPY --from=builder /usr/src/app/dist/webapp /usr/share/nginx/html
COPY nginx/conf.d/default.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

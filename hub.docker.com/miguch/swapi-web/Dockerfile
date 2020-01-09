FROM node:8 AS build

WORKDIR /usr/app

COPY ./package*.json ./

RUN npm install

COPY . .

RUN npm run webpack-build

FROM nginx:stable

COPY --from=build /usr/app/dist/ /var/www
COPY ./nginx.conf /etc/nginx/conf.d/default.conf
RUN echo "daemon off;" >> /etc/nginx/nginx.conf

EXPOSE 8082

CMD ["nginx"]
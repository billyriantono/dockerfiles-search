FROM node:8.11 as build
COPY . /client
RUN cd /client && npm install && npm run build

FROM nginx
COPY ./docker/nginx.conf /etc/nginx/nginx.conf
COPY --from=build /client/build/ /etc/nginx/html/

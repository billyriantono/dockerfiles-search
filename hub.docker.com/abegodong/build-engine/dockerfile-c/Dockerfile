FROM node:11.15.0-alpine as build
COPY . /app/
WORKDIR /app/
RUN yarn install
RUN yarn run build

# pro image
FROM nginx:1.17.0-alpine
RUN apk add --no-cache vim curl procps
COPY --from=build /app/default.conf /etc/nginx/mydefault.conf
COPY --from=build /app/dist/ /usr/share/nginx/html/
WORKDIR /
CMD envsubst '$cronus_ip $cronus_port' < /etc/nginx/mydefault.conf > /etc/nginx/conf.d/default.conf && nginx -g 'daemon off;'
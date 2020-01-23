FROM node:9.11.1-alpine
MAINTAINER HarveyHuang <service@68fen.com>

RUN apk add --no-cache nginx

WORKDIR /app
RUN cd /app
COPY . .
RUN npm install
ADD misc/nginx.conf /etc/nginx/nginx.conf
RUN npm run build
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

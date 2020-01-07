FROM node:6.1.0-wheezy
WORKDIR /app

RUN apt-get update && apt-get install -y nginx
RUN echo "daemon off;" >> /etc/nginx/nginx.conf

COPY redirects.d /etc/nginx/
COPY default /etc/nginx/sites-enabled/
COPY package.json /app/

RUN mkdir -p /app/out

RUN npm install --production

EXPOSE 8080
CMD nginx

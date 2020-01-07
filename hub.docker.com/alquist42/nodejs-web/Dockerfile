FROM node:alpine

LABEL Maintainer="Alexander Gefter <galaxy.gef@gmail.com>" \
      Description="Lightweight container with Nginx and Nodejs based on Alpine Linux."

# Install packages
RUN apk --update --no-cache add \
    nodejs-current \
    yarn \
    nginx \
    tini

# Configure nginx
COPY nginx /etc/nginx

# Entry point
COPY ./docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh

WORKDIR /usr/app
EXPOSE 8080
ENTRYPOINT ["/sbin/tini", "-g", "--", "/docker-entrypoint.sh"]

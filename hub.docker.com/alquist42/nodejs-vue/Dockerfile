FROM node:alpine

LABEL Maintainer="Alexander Gefter <galaxy.gef@gmail.com>" \
      Description="Lightweight container with Nginx, Vue CLI and Nodejs based on Alpine Linux."

# Install packages
RUN apk --update --no-cache add \
    nginx \
    tini

# Configure nginx
COPY nginx /etc/nginx

# Install Vue cli
RUN yarn global add @vue/cli

# Entry point
COPY ./docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh

WORKDIR /usr/app
EXPOSE 8080
ENTRYPOINT ["/sbin/tini", "-g", "--", "/docker-entrypoint.sh"]

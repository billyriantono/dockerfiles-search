ARG NODE_VERSION=10
ARG PHP_VERSION=7.2
FROM node:${NODE_VERSION}-slim
WORKDIR "/public_html"
RUN apt-get update

RUN npm install -g grunt-cli
RUN apt-get install php${PHP_VERSION} -y
RUN apt-get install -y \
      php${PHP_VERSION}-xml \
      php${PHP_VERSION}-dom \
      php${PHP_VERSION}-pdo \
      php${PHP_VERSION}-mysql \
      php${PHP_VERSION}-simplexml \
      php${PHP_VERSION}-mcrypt \
      php${PHP_VERSION}-intl \
      php${PHP_VERSION}-gd

COPY grunt-entrypoint /usr/local/bin/
RUN chmod +x /usr/local/bin/grunt-entrypoint
ENTRYPOINT ["grunt-entrypoint"]

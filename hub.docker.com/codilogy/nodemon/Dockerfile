FROM node:8-alpine
MAINTAINER Krzysztof Winiarski <info@codilogy.com>

# Install common libraries
RUN apk add --no-cache \
    su-exec

# Install nodemon
RUN mkdir -p /usr/lib/node_modules \
    && yarn global add nodemon pm2 lerna \
        --no-progress \
        --global-folder /usr/lib \
    && yarn cache clean \
    && chown -R node:node /usr/lib/node_modules \
    && rm -rf ~/.node-gyp /tmp/*

# Prepare workdir
RUN mkdir /app \
    && chown node:node /app
WORKDIR /app

# Entrypoint
ADD entrypoint.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]

# Default command
CMD ["nodemon"]

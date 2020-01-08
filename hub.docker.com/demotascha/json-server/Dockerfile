FROM node:lts-alpine

MAINTAINER WeiHao Huang <demotascha@gmail.com>

# Build a json-server image, and remove useless files
RUN npm install -g --production json-server  && \
    rm -rf /root/.npm                           \
    /usr/lib/node_modules/npm

# configure
EXPOSE 3000

# app directory
VOLUME /data
WORKDIR /data

# Define default command.
ENTRYPOINT ["json-server", "--watch", "db.json", "--host", "0.0.0.0"]
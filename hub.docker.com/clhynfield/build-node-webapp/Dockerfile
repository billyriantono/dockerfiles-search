FROM node:6.10-slim

MAINTAINER Clayton Hynfield <clayton@hynfield.org>

RUN yarn global add bower gulp && \
    yarn cache clean && \
    rm -rf /var/cache/* /tmp/*

WORKDIR /workspace

CMD [ "gulp" ]

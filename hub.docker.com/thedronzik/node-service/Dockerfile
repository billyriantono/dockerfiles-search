# Set the base image
FROM node:alpine

# File Author / Maintainer
MAINTAINER thedronzik <thedronzik@gmail.com>

# Install nodemon and Define working directory
RUN npm install -g nodemon &&\
    mkdir /app
WORKDIR /app

ONBUILD ADD . /app
ONBUILD RUN npm install

# Add startup script
ADD ./start.sh /start.sh
RUN chmod 755 /start.sh

RUN node -v && npm -v

# Entry point/ Run node with parameters from command configuration array
ENTRYPOINT ["/bin/sh", "/start.sh"]

FROM node:8
MAINTAINER Andrey Groza <andrey_groza@mail.ru>

RUN npm i -g create-react-app svgo

# Expose the port
EXPOSE 9000 35729

RUN mkdir /src
WORKDIR /src

USER node
CMD /bin/bash

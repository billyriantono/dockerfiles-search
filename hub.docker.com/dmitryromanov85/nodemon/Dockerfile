FROM node:10-alpine
MAINTAINER Dmitry Romanov "dmitry.romanov85@gmail.com"

RUN ["npm", "install", "-g", "nodemon"]

VOLUME ["/usr/src/app"]
WORKDIR /usr/src/app

ENTRYPOINT ["nodemon"]
CMD ["./bin/www"]

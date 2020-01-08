FROM node:11-alpine

MAINTAINER Marcel

VOLUME /app
WORKDIR /app

# node-sass requires build-base and python
RUN apk add --no-cache --update build-base python
RUN yarn global add @angular/cli

EXPOSE 4200

CMD ["ng", "serve", "--host", "0.0.0.0"]

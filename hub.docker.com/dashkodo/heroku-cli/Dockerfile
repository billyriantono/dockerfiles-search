FROM docker:latest

RUN apk update && apk --no-cache add curl nodejs nodejs-npm
RUN npm install -g heroku

CMD heroku

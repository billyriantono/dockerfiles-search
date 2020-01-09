FROM alpine

RUN apk add --update nodejs nodejs-npm

RUN npm install --global swagger-mock-validator

ENTRYPOINT ["swagger-mock-validator"]

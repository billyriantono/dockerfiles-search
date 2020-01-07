FROM openjdk:8-jdk-alpine3.8
RUN apk add --no-cache mongodb

VOLUME "/data/db"

EXPOSE 27017 28017

CMD [ "mongod" ]

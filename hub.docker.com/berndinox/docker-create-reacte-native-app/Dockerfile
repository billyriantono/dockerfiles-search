FROM node:alpine
MAINTAINER Bernd KLAUS "https://berndklaus.at"

WORKDIR /
RUN apk add --no-cache bash \
 && npm install -g create-react-native-app \
 && create-react-native-app app 
WORKDIR /app

EXPOSE 19000

CMD [ "yarn", "start" ]

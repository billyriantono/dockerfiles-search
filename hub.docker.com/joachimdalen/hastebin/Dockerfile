FROM node:12-alpine

LABEL maintainer="Joachim Dalen <joachim@dalenapps.no>" 

RUN apk -U upgrade \ 
    && apk add git

RUN git clone https://github.com/seejohnrun/haste-server.git /app

WORKDIR /app
RUN npm install

ADD ./app.sh /app/
RUN chmod 755 app.sh

EXPOSE 7777


CMD [ "./app.sh" ]
FROM node:10-alpine

RUN mkdir /ng-app
WORKDIR /ng-app

RUN mkdir /script
COPY run.sh /script/run.sh
RUN chmod +x /script/run.sh

CMD /script/run.sh
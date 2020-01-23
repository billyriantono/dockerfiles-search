FROM node:7

COPY *.json /data/sms-api/
COPY *.yaml /data/sms-api/
COPY yarn.lock /data/sms-api/
COPY src/ /data/sms-api/src
COPY typings/ /data/sms-api/typings

RUN cd /data/sms-api && yarn --pure-lockfile
RUN cd /data/sms-api && yarn build

EXPOSE 4003

USER root
WORKDIR /data/sms-api
ENV NODE_ENV production

CMD ["npm", "run", "start:production"]

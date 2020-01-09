FROM node:8.9.4

ENV APPNAME dusnow
ENV PORT 8080

RUN mkdir -p /usr/local/nodejs
WORKDIR /usr/local/nodejs
COPY . /usr/src/nodejs

WORKDIR /usr/src/nodejs/${APPNAME}
RUN yarn
RUN yarn build 

EXPOSE ${PORT}

CMD yarn start
FROM alpine

RUN apk add --update nodejs nodejs-npm
RUN npm install -g http-server

CMD ["http-server", "/static"]

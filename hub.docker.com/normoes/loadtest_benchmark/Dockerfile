FROM alpine:3.10

RUN apk update && apk --no-cache add nodejs nodejs-npm \
    && npm install -g loadtest

ENTRYPOINT ["sh"]

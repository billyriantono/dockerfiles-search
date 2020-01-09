FROM node:lts-alpine

LABEL maintainer "shinyay <shinya.com@gmail.com>"

RUN apk --no-cache add \
    build-base \
    python \
    gcc \
    --update make \
    && npm install -g node-gyp terminalizer --unsafe-perm

ENTRYPOINT [ "terminalizer" ]

CMD [ "--help" ]

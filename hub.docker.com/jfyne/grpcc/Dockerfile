from znly/protoc

WORKDIR /proto

RUN apk add --no-cache --virtual deps git && \
    apk add --no-cache nodejs nodejs-npm && \
    npm install --unsafe-perm -g jfyne/grpcc && \
    apk del deps

ENTRYPOINT ["grpcc"]

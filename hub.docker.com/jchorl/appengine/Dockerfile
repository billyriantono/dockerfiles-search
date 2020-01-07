FROM golang:alpine

RUN apk update && \
    # for wget and ssl
    apk add wget ca-certificates && \
    apk add unzip && \
    apk add python && \
    # for go get
    apk add git

RUN wget https://storage.googleapis.com/appengine-sdks/featured/go_appengine_sdk_linux_amd64-1.9.38.zip -O /appengine.zip && \
    unzip /appengine.zip -d / && \
    rm /appengine.zip

ENV PATH /go_appengine/:$PATH
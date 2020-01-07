FROM golang:1.6.0-alpine

RUN apk update && apk add curl bash \
  && curl -SL https://github.com/odise/go-cron/releases/download/v0.0.7/go-cron-linux.gz \
    | zcat > /usr/local/bin/go-cron \
  && chmod u+x /usr/local/bin/go-cron \
  && rm -rf /var/cache/apk/*

RUN mkdir -p /go/src/app
WORKDIR /go/src/app

ONBUILD COPY . /go/src/app
ONBUILD RUN go get -v -d
ONBUILD RUN go install -v

ENV SCHEDULE ${SCHEDULE:-* * * * * *}

COPY run.sh /usr/local/bin/

EXPOSE 18080

ENTRYPOINT ["run.sh"]
CMD ["run.sh"]

FROM golang:alpine

RUN apk update \
 && apk --no-cache add ca-certificates openssl git \
 && update-ca-certificates

ENV DOCKERIZE_VERSION v0.3.0
RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
 && tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
 && rm dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz

RUN go get github.com/justwatchcom/sql_exporter

COPY ./templates/config.tmpl /config/config.tmpl

ENTRYPOINT ["dockerize", "-template", "/config/config.tmpl:/config/config.yml"]
CMD ["/go/bin/sql_exporter", "--web.listen-address", "0.0.0.0:9237", "--config.file", "/config/config.yml"]

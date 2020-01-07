FROM alpine:3.10

ENV VERSION v4.5.0

RUN apk add --no-cache curl

RUN curl -L https://github.com/golang-migrate/migrate/releases/download/${VERSION}/migrate.linux-amd64.tar.gz | tar xvz -C /usr/local/bin && \
  mv /usr/local/bin/migrate.linux-amd64 /usr/local/bin/migrate

ENTRYPOINT [ "migrate" ]

CMD [ "--help" ]

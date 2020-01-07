FROM alpine:3.10
MAINTAINER Richard Kojedzinszky <richard@kojedz.in>

RUN apk --no-cache add postgresql-client

RUN ln -s /tmp/.pgpass /

USER nobody

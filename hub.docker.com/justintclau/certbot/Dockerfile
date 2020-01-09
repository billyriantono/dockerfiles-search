FROM alpine:edge

MAINTAINER Pierre Prinetti <me@qrawl.net>

RUN apk add --update bash certbot

COPY ./run.sh /run.sh

RUN chmod +x /run.sh

CMD ["/run.sh"]

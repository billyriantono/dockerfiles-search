FROM alpine:3.8

RUN apk update \
    && apk add python py-pip \
    && pip install awscli

COPY run.sh /run.sh

RUN chmod 755 /run.sh

CMD ["/run.sh"]

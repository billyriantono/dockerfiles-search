FROM alpine:latest
MAINTAINER Christopher Emerson <christopher.emerson@whiteoaksecurity.com>

RUN apk add --update python-dev py-pip gcc musl-dev \
&&  rm -f /var/cache/apk/*

RUN pip install sslyze

RUN mkdir /output
VOLUME ["/output"]
WORKDIR /output

ENTRYPOINT ["sslyze"]

CMD ["-h"]

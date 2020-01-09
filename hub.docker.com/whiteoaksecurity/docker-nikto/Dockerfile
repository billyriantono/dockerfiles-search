FROM alpine:latest
MAINTAINER Christopher Emerson <christopher.emerson@whiteoaksecurity.com>

RUN apk add --update perl openssl perl-net-ssleay wget git \
&&    rm -f /var/cache/apk/* 

RUN	git clone https://github.com/sullo/nikto.git

RUN mkdir /output
VOLUME ["/output"]
WORKDIR /nikto/program

ENTRYPOINT ["perl", "nikto.pl"]

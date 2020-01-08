FROM alpine:3.10

MAINTAINER Charlie Kim <kimcharli@gmail.com>

RUN apk add openssl

WORKDIR /work

ADD run_create.sh /run_create.sh

CMD ["sh", "/run_create.sh"]




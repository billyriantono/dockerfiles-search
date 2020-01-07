FROM alpine:3.3
MAINTAINER Harshad Yeola <harshadyeola92@gmail.com>

RUN apk update && apk upgrade && \
    apk add --no-cache bash git openssh
VOLUME /code
COPY ./entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]

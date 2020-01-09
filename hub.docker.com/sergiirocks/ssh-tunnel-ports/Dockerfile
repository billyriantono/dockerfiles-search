FROM alpine:3.6
LABEL maintainer="docker@naumov.pw"

VOLUME /root/.ssh

RUN apk add --update openssh-client bash && rm -rf /var/cache/apk/*

COPY docker-entrypoint.sh /

CMD [ "/docker-entrypoint.sh" ]

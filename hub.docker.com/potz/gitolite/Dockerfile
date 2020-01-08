FROM alpine:3.3

MAINTAINER Potiguar Faga <potz@potz.me>

RUN apk add --update gitolite openssh \
    && passwd -u git \
    && rm -rf /var/cache/apk/*

COPY start.sh /

VOLUME /etc/ssh
VOLUME /var/lib/git
EXPOSE 22

CMD [ "sshd" ]
ENTRYPOINT [ "/start.sh" ]

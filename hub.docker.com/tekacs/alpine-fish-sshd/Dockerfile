FROM sickp/alpine-sshd

MAINTAINER Amar Sood (@tekacs)

RUN apk update && \
    apk add --no-cache fish man mdocml-apropos bc && \
    rm -f /tmp/* /etc/apk/cache/*

RUN sed -i -e "s/bin\/ash/usr\/bin\/fish/" /etc/passwd
RUN passwd -d root

ENV SHELL /usr/bin/fish

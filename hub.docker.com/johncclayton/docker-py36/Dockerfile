FROM python:3.6-alpine
MAINTAINER John Clayton johnclayton72@gmail.com
LABEL Description="alpine python 3.6 openssh server - maybe"

VOLUME /data
EXPOSE 22 443

RUN apk --update add tzdata openssh bash netcat-openbsd sudo busybox-suid && \
    cp -f /usr/share/zoneinfo/Europe/Zurich /etc/localtime && \
    echo "Europe/Zurich" > /etc/timezone && \
    date && \
    mkdir -p ~root/.ssh && chmod 700 ~root/.ssh/ && \
    echo -e "Port 22\n" >> /etc/ssh/sshd_config && \
    cp -a /etc/ssh /etc/ssh.cache && \
    rm -rf /var/cache/apk/*

RUN  apk add --no-cache bash git openssh

RUN addgroup dev \
    && adduser  -G dev -s /bin/sh -D dev \
    && echo "dev:r" | /usr/sbin/chpasswd \
    && echo "dev    ALL=(ALL) ALL" >> /etc/sudoers

ADD chroot /

ENTRYPOINT ["/usr/local/bin/entry.sh"]

CMD ["/usr/sbin/sshd", "-D", "-f", "/etc/ssh/sshd_config"]

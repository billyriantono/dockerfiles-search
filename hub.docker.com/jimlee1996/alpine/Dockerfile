FROM alpine:latest
MAINTAINER JimLee1996 <59061463@qq.com>

RUN apk add --no-cache openssh

RUN echo 'root:admin' | chpasswd

RUN sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config

RUN mkdir -p /var/run/sshd

EXPOSE 22

CMD    ["/usr/sbin/sshd", "-D"]

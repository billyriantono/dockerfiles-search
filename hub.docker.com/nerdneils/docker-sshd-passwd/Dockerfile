FROM alpine
MAINTAINER dengqi
ENV PASSWD rootpassword
RUN apk update && apk add --no-cache openssh && \
    echo "Port 22" >> /etc/ssh/sshd_config  &&\
    echo "PermitRootLogin yes" >> /etc/ssh/sshd_config &&\
    echo "root:$PASSWD" | chpasswd && ssh-keygen -A
EXPOSE 22
CMD ["/usr/sbin/sshd","-D","-f","/etc/ssh/sshd_config"]
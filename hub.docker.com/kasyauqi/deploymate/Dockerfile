FROM alpine:latest
MAINTAINER Reza Kasyauqi Sabhara <kasyauqi@gmail.com>

RUN apk --update add --no-cache openssh \
  && ssh-keygen -A \
  && sed -i s/#PermitRootLogin.*/PermitRootLogin\ yes/ /etc/ssh/sshd_config \
  && echo "root:root" | chpasswd \
  && rm -rf /var/cache/apk/*

EXPOSE 22
CMD ["/usr/sbin/sshd","-D"]

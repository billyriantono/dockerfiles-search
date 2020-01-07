FROM alpine:3.9
MAINTAINER from www.beyondspider.com by admin (admin@beyondspider.com)

ENV TIME_ZONE Asia/Shanghai
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories
RUN apk update && \
    apk add --no-cache openssh-server tzdata pwgen && \
	ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key && \
    ssh-keygen -t rsa -f /etc/ssh/ssh_host_ecdsa_key && \
    ssh-keygen -t rsa -f /etc/ssh/ssh_host_ed25519_key && \
    sed -i "s/#PermitRootLogin.*/PermitRootLogin yes/g" /etc/ssh/sshd_config && \
	ln -sf /usr/share/zoneinfo/${TIME_ZONE} /etc/localtime

ADD run.sh /run.sh
ADD password.sh /password.sh

RUN chmod 777 /*.sh
EXPOSE 22
CMD ["/run.sh"]

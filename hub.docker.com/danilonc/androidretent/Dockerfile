ARG         ALPINE_VERSION=${ALPINE_VERSION:-3.8}
FROM        alpine:${ALPINE_VERSION}

LABEL       maintainer="https://github.com/DanielNeto"

ARG         OPENSSH_VERSION=${OPENSSH_VERSION:-7.7_p1-r4}
ENV         OPENSSH_VERSION=${OPENSSH_VERSION}

##Install ssh and iperf packets
RUN         apk update && \
            apk upgrade && \
            apk add openssh=${OPENSSH_VERSION} && \
            apk add iperf && \
            mkdir -p /root/.ssh && \
            rm -rf /var/cache/apk/* /tmp/*

##Generate host keys if not presente
RUN         ssh-keygen -A

##Enable root login
RUN         sed -i s/#PermitRootLogin.*/PermitRootLogin\ yes/ /etc/ssh/sshd_config

##Set root password as root
RUN         echo "root:root" | chpasswd

EXPOSE      22
VOLUME      ["/etc/ssh"]
CMD         /usr/sbin/sshd -D

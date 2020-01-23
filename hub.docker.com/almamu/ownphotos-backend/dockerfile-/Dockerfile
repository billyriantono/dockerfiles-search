from ubuntu:artful

MAINTAINER alljoynsville

RUN DEBIAN_FRONTEND=noninteractive apt-get -yqq update \
 && DEBIAN_FRONTEND=noninteractive apt-get -yqq install openssh-server dropbear-bin net-tools curl \
 && mkdir /var/run/sshd \
 && useradd -m sshuser -s /bin/bash -u 1001 \
 && mkdir /home/sshuser/.ssh \
 && chown -R sshuser:sshuser /home/sshuser/.ssh \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 22/tcp

CMD ["/usr/sbin/sshd", "-D"]

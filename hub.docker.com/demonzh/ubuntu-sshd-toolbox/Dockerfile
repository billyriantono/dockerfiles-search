FROM ubuntu:18.10
LABEL maintainer="Silent Applause"

RUN apt-get update &&  \
    apt-get install -y openssh-server vim curl wget dnsutils telnet && \
    mkdir /var/run/sshd  && \
    echo 'root:123456' |chpasswd  && \
    sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config  && \
    sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config  && \
    mkdir /root/.ssh  && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    echo "alias vi='vim'" >>/root/.bashrc
EXPOSE 22
CMD    ["/usr/sbin/sshd", "-D"]
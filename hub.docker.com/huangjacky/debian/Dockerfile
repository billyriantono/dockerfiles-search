FROM debian
MAINTAINER huangjacky<huangjacky@163.com>
COPY sources.list /etc/apt/sources.list
# COPY sysctl.conf /etc/sysctl.conf
RUN export DEBIAN_FRONTEND=noninteractive && \
    apt-get update && apt-get upgrade -y && apt-get dist-upgrade -y && apt-get install -y vim net-tools socat wget tzdata procps && \
    apt-get clean && apt-get autoremove -y && \
    ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    dpkg-reconfigure tzdata && \
    echo "* soft    nofile  65535\n*    hard    nofile 65536" >> /etc/security/limits.conf
CMD [ "/bin/bash" ]


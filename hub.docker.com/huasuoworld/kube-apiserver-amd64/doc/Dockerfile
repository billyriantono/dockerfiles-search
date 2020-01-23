FROM ubuntu
MAINTAINER huangjacky<huangjacky@163.com>
COPY sources.list /etc/apt/sources.list
RUN export DEBIAN_FRONTEND=noninteractive && \
    apt-get update && apt-get upgrade -y && apt-get dist-upgrade -y && apt-get install -y vim net-tools socat wget tzdata && \
    apt-get clean && apt-get autoremove -y && \
    ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
CMD [ "/bin/bash" ]
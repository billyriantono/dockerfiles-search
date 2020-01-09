FROM ubuntu

ADD dist /root/dist

RUN sed -i s@/archive.ubuntu.com/@/mirrors.aliyun.com/@g /etc/apt/sources.list && \
    apt update && \
    apt install -y dante-server && \
    mv /root/dist/danted.conf /etc/ && \
    useradd -p '$1$saltt$VxQLDjsVwFr4r6oYc8sj31' -s /usr/sbin/nologin -M lili && \
    rm -rf /var/cache/apt

CMD danted

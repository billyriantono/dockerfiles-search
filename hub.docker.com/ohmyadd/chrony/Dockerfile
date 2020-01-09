FROM ubuntu

RUN sed -i 's/http:\/\/archive.ubuntu.com\/ubuntu\//http:\/\/mirrors.163.com\/ubuntu\//g' /etc/apt/sources.list && \
    apt update && \
    apt install -y --no-install-recommends chrony && \
    echo 'allow 0.0.0.0/0' >> /etc/chrony/chrony.conf && \
    rm -rf /var/cache/apt/*
EXPOSE 123/udp

ENTRYPOINT chronyd -n

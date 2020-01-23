FROM python:2.7.15-alpine3.7
WORKDIR /root

COPY start.sh /root/start.sh
RUN apk update && apk add git libffi libffi-dev gcc g++ make openssl-dev openssl openssh python3 && \
    cd /root/ && git clone https://github.com/evait-security/CrackMapExec && \
    cd /root/CrackMapExec && git submodule init && git submodule update --recursive && \
    python setup.py install &&  apk del git libffi-dev gcc g++ make openssl-dev && \
    pip3 install pypykatz && \
    rm -rf /var/cache/apk/*
CMD ["/bin/sh","/root/start.sh"]

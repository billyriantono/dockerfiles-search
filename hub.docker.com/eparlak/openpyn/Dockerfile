FROM ubuntu:18.04
ENV COUNTRY ch
WORKDIR /usr/local/lib/python3.6/dist-packages/openpyn/
RUN apt update &&\
    apt install -y openvpn unzip wget python3-setuptools python3-pip sudo iputils-ping &&\
    python3 -m pip install --upgrade openpyn &&\
    wget https://downloads.nordcdn.com/configs/archives/servers/ovpn.zip &&\
    unzip -q -u -o /usr/local/lib/python3.6/dist-packages/openpyn/ovpn.zip -d /usr/local/lib/python3.6/dist-packages/openpyn/files/ &&\
    rm ovpn.zip &&\
    mkdir /var/log/openpyn &&\
    chmod 770 /var/log/openpyn &&\
    rm -rf /var/lib/apt/lists/*
COPY docker-entrypoint /usr/local/bin/
ENTRYPOINT ["docker-entrypoint"]
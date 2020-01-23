FROM ubuntu:16.04

RUN apt update && apt upgrade -y && apt install -y software-properties-common ca-certificates wget curl ssh jq zip curl openssl libtool libtool-bin iputils-ping dnsutils python build-essential automake bison libglib2.0-dev screen
RUN apt install -y python3 python3-dev python3-pip python3-virtualenv python-pip python-dev && pip3 install --no-cache-dir gevent==1.2.1 flask==0.12

ENV FLASK_PROXY_PORT 8080

RUN mkdir -p /actionProxy
ADD actionproxy.py /actionProxy/

RUN mkdir -p /action

CMD ["/bin/bash", "-c", "cd actionProxy && python3 -u actionproxy.py"]

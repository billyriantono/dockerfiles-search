FROM ubuntu:latest

RUN apt-get update
RUN apt-get install -y python-pip python-m2crypto
RUN pip install shadowsocks

ENV SS_SERVER_ADDR 0.0.0.0
ENV SS_SERVER_PORT 8388
ENV SS_PASSWORD password
ENV SS_METHOD aes-256-cfb
ENV SS_TIMEOUT 300

ADD run.sh /run.sh
RUN chmod 755 /*.sh

EXPOSE $SS_SERVER_PORT

CMD ["/run.sh"]

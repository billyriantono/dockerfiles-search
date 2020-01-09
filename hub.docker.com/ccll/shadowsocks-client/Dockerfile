FROM python:3.6.2

RUN pip install --no-cache-dir shadowsocks

VOLUME /opt/shadowsocks
EXPOSE 1080

ADD run-sslocal.sh /opt/shadowsocks/run-sslocal.sh

CMD ["bash", "/opt/shadowsocks/run-sslocal.sh"]


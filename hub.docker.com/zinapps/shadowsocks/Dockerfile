FROM alpine

RUN apk update && \
    apk add --no-cache py-pip git

RUN pip install -U git+https://github.com/shadowsocks/shadowsocks.git@master

COPY start.sh /opt/start.sh
RUN chmod +x /opt/start.sh

CMD ["/opt/start.sh"]

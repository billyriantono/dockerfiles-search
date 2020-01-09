FROM alpine:3.6

ENV SS_SERVER_PORT 50080
ENV SS_PASSWORD 1q2w3e4r
ENV SS_METHOD aes-128-cfb

RUN apk add --update py-pip && \
	pip install --upgrade pip && \
	pip install shadowsocks
COPY entrypoint.sh /
ENTRYPOINT ["sh", "/entrypoint.sh"]

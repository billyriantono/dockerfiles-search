FROM alpine:latest
MAINTAINER Timmy Zhu <zhu327@gmail.com>

RUN apk add --update --no-cache bash py2-pip

RUN pip install shadowsocks

ENV SERVER 0.0.0.0
ENV PORT 443
ENV PASSWORD GRGyU4bSs8KyI8eI
ENV METHOD aes-128-cfb
ENV TIMEOUT 600

COPY entrypoint.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/entrypoint.sh

EXPOSE $PORT

ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]

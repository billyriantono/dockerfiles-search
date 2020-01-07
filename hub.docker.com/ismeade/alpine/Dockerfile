FROM alpine:3.6

MAINTAINER ismeade <ismeade99@sina.com>

ENV LANG=C.UTF-8

RUN apk add --no-cache --update-cache bash tzdata && \
    cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    echo "Asia/Shanghai" > /etc/timezone && \
    apk del tzdata

CMD ["/bin/bash"]

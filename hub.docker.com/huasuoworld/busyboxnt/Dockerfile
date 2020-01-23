# ==============================================================================
# 基础 alpine
# 
# 替换源为阿里源，设置中国时区，安装bash
# ==============================================================================

FROM alpine:latest

MAINTAINER homesheer <homesheer@gmail.com>

ARG TZ="Asia/Shanghai"

ENV TZ ${TZ}

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/' /etc/apk/repositories

RUN apk update \
    apk upgrade \
    && apk add --no-cache bash tzdata \
    && ln -sf /usr/share/zoneinfo/${TZ} /etc/localtime \
    && echo ${TZ} > /etc/timezone

CMD ["/bin/bash"]

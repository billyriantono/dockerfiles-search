FROM ubuntu:18.04

ENV LANG C.UTF-8
ENV TZ 'Asia/Shanghai'
ENV EFB_DATA_PATH /data/
ENV EFB_PARAMS ""
ENV EFB_PROFILE "default"
ENV HTTPS_PROXY ""

RUN apt-get update && apt-get --fix-missing install -y \
    python3 python3-pip git ffmpeg && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
RUN pip3 install ehforwarderbot efb-telegram-master efb-wechat-slave efb-gpg-middleware
RUN pip3 install git+https://github.com/zhangzhishan/efb-filter-middleware

ADD entrypoint.sh /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]

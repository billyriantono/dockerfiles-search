FROM selenium/hub

MAINTAINER madehao1983@sina.com

USER root
RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y locales \
    && apt-get clean \
    && rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/* \
    && localedef -f UTF-8 -i zh_CN zh_CN.UTF-8

USER seluser
ENV TZ="Asia/Shanghai"
ENV LANG="zh_CN.UTF-8"

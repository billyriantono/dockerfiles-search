FROM selenium/node-chrome

MAINTAINER madehao1983@sina.com

USER root
RUN localedef -f UTF-8 -i zh_CN zh_CN.UTF-8 \

    && echo "Asia/Shanghai" | tee /etc/timezone \
    && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

USER seluser
ENV TZ="Asia/Shanghai" \
    LANG="zh_CN.UTF-8"

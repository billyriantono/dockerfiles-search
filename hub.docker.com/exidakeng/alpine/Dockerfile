FROM alpine:3.10

# 更新Alpine的软件源为国内（清华大学）的站点
RUN echo "https://mirror.tuna.tsinghua.edu.cn/alpine/v3.10/main/" > /etc/apk/repositories \
    && apk update \
    && apk upgrade \
    && apk add --no-cache bash \
    bash-doc \
    bash-completion \
    && apk add -U tzdata \
    && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && apk del tzdata \
    && rm -rf /var/cache/apk/* \
    && /bin/bash \
    && echo 'alias ll="ls -alh"' >> /root/.bashrc

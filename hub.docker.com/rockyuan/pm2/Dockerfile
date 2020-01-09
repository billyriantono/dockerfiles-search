FROM keymetrics/pm2:latest-alpine

LABEL name='pm2' tag='onbuild' maintainer='RockYuan <RockYuan@gmail>'

ENV BUILD_DEPS \
    tzdata

ENV RUN_DEPS \
    curl \
    git \
    bash \
    vim

RUN set -xe \
    && apk update \
    && apk add --no-cache --virtual .build-deps \
        ${BUILD_DEPS} \
    && apk add --no-cache --virtual .run-deps \
        ${RUN_DEPS} \
    && cp /usr/share/zoneinfo/Asia/Hong_Kong /etc/localtime \
    && echo "Asia/Hong_Kong" > /etc/timezone \
    && apk del .build-deps \
    && rm -rf /tmp/* \
    && mkdir -p /data

# 根据系统环境变量修改命令行提示
COPY config/env_prompt.sh /etc/profile.d/env_prompt.sh
ENV ENV="/etc/profile"

# 通过ONBUILD文件可定制安装需要的包和依赖包,txt文件每行一个包名
# dependencies.txt 编译时需要的包,最后会卸装
# packages.txt 运行时需要的包,会保留下来
# requirements.txt NPM全局安装的扩展
ONBUILD ADD ./pm2-onbuild/*.txt /tmp/
ONBUILD RUN cd /tmp; \
    [ -f packages.txt -o -f dependencies.txt ] && apk update; \
    [ -f dependencies.txt ] && xargs -r apk add --no-cache < dependencies.txt; \
    [ -f packages.txt ] && xargs -r apk add --no-cache < packages.txt; \
    [ -f requirements.txt ] && xargs -r npm install -g < requirements.txt; \
    [ -f dependencies.txt ] && xargs -r apk del < dependencies.txt; \
    [ -f packages.txt -o -f dependencies.txt ] && rm -rf /tmp/*
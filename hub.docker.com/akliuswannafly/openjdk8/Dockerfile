FROM openjdk:8
MAINTAINER Apollos

RUN apt-get update \
    && apt-get install -y locales \
    && rm -rf /var/lib/apt/lists/* \
    && localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8 \
    && rm -rf /etc/localtime \
    && ln -s /usr/share/zoneinfo/Asia/Harbin /etc/localtime
ENV LANG en_US.utf8

ONBUILD COPY ./*.zip /release/

ONBUILD RUN cd /release \
    && unzip *.zip \
    && rm *.zip \
    && cd `ls`/bin \
    && ln -s `pwd`/`ls | sed -n '1p'` /entrypoint

ONBUILD CMD ["/entrypoint", "-Dconfig.resource=prod.conf", "-Dfile.encoding=UTF8"]

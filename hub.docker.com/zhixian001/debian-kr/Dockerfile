FROM debian:jessie

LABEL maintainer="zhixian001"\
    version="1.0"

ENV TZ=Asia/Seoul

RUN sed -i 's/deb.debian.org/ftp.harukasan.org/g' /etc/apt/sources.list && \
    apt-get update && \
    apt-get install -y locales && \
    rm -rf /var/lib/apt/lists/* && \
    echo "ko_KR.UTF-8 UTF-8" >> /etc/locale.gen && \
    locale-gen && \
    localedef -i ko_KR -c -f UTF-8 -A /usr/share/locale/locale.alias ko_KR.UTF-8 && \
    ln -snf "/usr/share/zoneinfo/${TZ}" /etc/localtime && \
    echo "${TZ}" > /etc/timezone

ENV LANG="ko_KR.UTF-8" \
    LANGUAGE="ko_KR.UTF-8" \
    LC_ALL="ko_KR.UTF-8"

ENTRYPOINT [ "/bin/bash" ]

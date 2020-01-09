FROM debian:buster
MAINTAINER Lex White <t7k312@gmail.com>

ENV YD_REPO="deb http://repo.yandex.ru/yandex-disk/deb/ stable main" \
    YANDEX_DIR="/yandex" \
    YANDEX_USER="yandex" \
    YANDEX_PASS="yandex" \
    UID="1000" \
    GID="1000"

RUN groupadd -g $GID yandex \
    && useradd -u $UID -r -g $GID -m -s /sbin/nologin \
        -c "Yandex.Disk Application User" yandex

# Install APP
RUN apt update && apt install -y \
       wget \
       gnupg \
    && echo $YD_REPO > /etc/apt/sources.list.d/yandex-disk.list \
    && wget http://repo.yandex.ru/yandex-disk/YANDEX-DISK-KEY.GPG -O- | apt-key add - \
    && apt update && apt install -y \
        yandex-disk \
    # Delete trash
    && apt autoclean \
    && rm -rf /var/lib/apt/lists/*

# Ports\user\volume
VOLUME $YANDEX_DIR

# Exec
USER yandex
COPY entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]

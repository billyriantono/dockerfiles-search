FROM debian:stretch

LABEL maintainer="Jason Raimondi <jason@raimondi.us>"

WORKDIR /usr/local/src

ENV GEARMAN_VERSION="1.1.17"
ENV GEARMAN_URL="https://github.com/gearman/gearmand/releases/download/$GEARMAN_VERSION/gearmand-$GEARMAN_VERSION.tar.gz" \
    BUILD_DEPENDENCIES="\
        autoconf \
        ca-certificates \
		dpkg-dev \
		file \
		g++ \
		gcc \
		libc-dev \
		make \
		pkg-config \
        \
        wget\
        " \
    RUN_DEPENDENCIES="\
        libboost-all-dev \
        libevent-dev \
        bison \
        flex \
        libtool \
        uuid-dev \
        gperf \
        "

USER root

RUN apt-get update \
    && apt-get install -y --no-install-recommends $BUILD_DEPENDENCIES $RUN_DEPENDENCIES \
    \
    && wget -q $GEARMAN_URL -O gearmand.tar.gz \
    && mkdir /usr/local/src/gearmand \
    && tar zxf gearmand.tar.gz -C /usr/local/src/gearmand --strip-components=1 \
    && ( \
        cd /usr/local/src/gearmand \
        && ./configure --with-lib-dir=/usr/lib/x86_64-linux-gnu \
        && make \
        && make install \
    ) \
    && rm gearmand.tar.gz \
    \
    && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false $BUILD_DEPENDENCIES \
    && apt-get clean \
    \
    && groupadd -r gearman \
    && useradd -r -g gearman -s /sbin/nologin gearman \
    && mkdir -p /var/log/gearman \
    && chown gearman:gearman /var/log/gearman

EXPOSE 4730

USER gearman

CMD ["gearmand","--log-file", "/var/log/gearman/gearmand.log", "-p", "4730", "-L", "0.0.0.0"]

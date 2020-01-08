FROM project42/syslog-alpine:3.8

ENV WEEWX_VERSION=3.9.2
ENV BELCHERTOWN_VERSION=1.0.1
ENV INIGO_VERSION=0.7.1
ENV MQTT_VERSION=0.19
ENV WEATHERBUG_VERSION=0.6
ENV WEATHERCLOUD_VERSION=0.11

# imperial or metric
ENV INIGO_UNITS=imperial
    
ENV WEEWX_URL=http://weewx.com/downloads/weewx-$WEEWX_VERSION.tar.gz
ENV BELCHERTOWN_URL=https://github.com/poblabs/weewx-belchertown/releases/download/weewx-belchertown-$BELCHERTOWN_VERSION/weewx-belchertown-release-$BELCHERTOWN_VERSION.tar.gz
ENV INTERCEPTOR_URL=https://github.com/matthewwall/weewx-interceptor/archive/master.zip
ENV INFLUX_URL=https://github.com/matthewwall/weewx-influx/archive/master.zip
ENV INIGO_URL=https://github.com/evilbunny2008/weeWXWeatherApp/releases/download/$INIGO_VERSION/inigo-$INIGO_UNITS.tar.gz
ENV SFTP_URL=https://github.com/matthewwall/weewx-sftp/archive/master.zip
ENV MQTT_URL=http://lancet.mit.edu/mwall/projects/weather/releases/weewx-mqtt-$MQTT_VERSION.tgz
ENV WEATHERBUG_URL=http://lancet.mit.edu/mwall/projects/weather/releases/weewx-wbug-$WEATHERBUG_VERSION.tgz
ENV WEATHERCLOUD_URL=http://lancet.mit.edu/mwall/projects/weather/releases/weewx-wcloud-$WEATHERCLOUD_VERSION.tgz
ENV WINDY_URL=https://github.com/matthewwall/weewx-windy/archive/master.zip

RUN set -ex; \
    apk --no-cache --update upgrade; \
    apk add --no-cache \
        py2-pillow \
        py2-configobj \
        mariadb-client \
        rsync \
        tzdata \
        py-paho-mqtt \
        py-cffi \
        py-cheetah \
        py-six \
        py-paramiko \
        py-cryptography \
        py-mysqldb; \
    apk add --no-cache --virtual .build-deps \
        py2-pip \
        python2-dev \
        build-base; \
    pip install --no-cache-dir \
        pyephem \
        pysftp; \
    cd /tmp; \
    wget $WEEWX_URL -O weewx.tar.gz; \
    tar xvf weewx.tar.gz; \
    cd weewx-$WEEWX_VERSION; \
    ./setup.py install --no-prompt -O2; \
    wget -O /tmp/weewx-interceptor.zip $INTERCEPTOR_URL; \
    wget -O /tmp/weewx-influx.zip $INFLUX_URL; \
    wget -O /tmp/weewx-belchertown.tgz $BELCHERTOWN_URL; \
    wget -O /tmp/weewx-inigo.tgz $INIGO_URL; \
    wget -O /tmp/weewx-sftp.zip $SFTP_URL; \
    wget -O /tmp/weewx-mqtt.tgz $MQTT_URL; \
    wget -O /tmp/weewx-weatherbug.tgz $WEATHERBUG_URL; \
    wget -O /tmp/weewx-weathercloud.tgz $WEATHERCLOUD_URL; \
    wget -O /tmp/weewx-windy.zip $WINDY_URL; \
    cd /home/weewx; \
    bin/wee_extension --install /tmp/weewx-interceptor.zip; \
    bin/wee_extension --install /tmp/weewx-belchertown.tgz; \
    bin/wee_extension --install /tmp/weewx-influx.zip; \
    bin/wee_extension --install /tmp/weewx-inigo.tgz; \
    bin/wee_extension --install /tmp/weewx-sftp.zip; \
    bin/wee_extension --install /tmp/weewx-mqtt.tgz; \
    bin/wee_extension --install /tmp/weewx-weatherbug.tgz; \
    bin/wee_extension --install /tmp/weewx-weathercloud.tgz; \
    bin/wee_extension --install /tmp/weewx-windy.zip; \
    rm -rf /tmp/* ; \
    apk del --no-cache .build-deps; \
    mkdir -p /home/weewx/config; \
    cp /home/weewx/weewx.conf /home/weewx/config/
    
VOLUME ["/home/weewx/public_html", "/home/weewx/config"]

CMD ["/home/weewx/bin/weewxd", "-x", "/home/weewx/config/weewx.conf"]

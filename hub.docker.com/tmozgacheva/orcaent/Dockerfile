FROM python:3.6
MAINTAINER TIKI SRE <sre@tiki.vn>

ENV DEBIAN_FRONTEND=noninteractive TZ=Asia/Saigon
ENV APP_HOME=/app APP_USER=tiki APP_GRP=tiki
ENV NEW_RELIC_CONFIG_FILE=newrelic.ini NEW_RELIC_LICENSE_KEY=license_key NEW_RELIC_APP_NAME=app_name
ENV PIP_NO_CACHE_DIR=0 GUNICORN_WORKER=4

COPY requirements.txt /tmp/requirements.txt

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
    && echo $TZ > /etc/timezone \
    && groupadd -g 701 "${APP_GRP}" \
    && useradd -u 701 -m -d "${APP_HOME}" -s /bin/bash -g "${APP_GRP}" "${APP_USER}" \
    && chown -R "${APP_USER}":"${APP_GRP}" "${APP_HOME}" \
    && apt-get -qq -y update \
    && apt-get install -qq --no-install-recommends -y \
        supervisor curl jq vim-nox moreutils gettext-base \
        locales tzdata lsb-release \
    && pip install --upgrade --no-cache-dir pip \
    && pip install --no-cache-dir -r /tmp/requirements.txt \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY config /etc/
COPY entrypoint.sh /entrypoint.sh

WORKDIR ${APP_HOME}
EXPOSE 8080
CMD ["/entrypoint.sh"]

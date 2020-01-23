FROM nginx:alpine

RUN set -x \
 && apk update \
 && apk add --update  bash \
                      curl \
                      zip \
                      tar \
                      openssl \
                      supervisor \
                      gettext \
                      openssh \
                      nano \
                      git \
                      pwgen \
                      dcron

# SUPERVISOR SETUP

VOLUME ["/etc/supervisor/conf.d"]

ARG SUPERVISOR_USER
ARG SUPERVISOR_PASS
ARG CRON_FILE
ARG CONFIG_DIR

ENV SUPERVISOR_USER supervisoradmin
ENV CONFIG_DIR /etc/supervisor_config


RUN mkdir -p /var/log/supervisor \
  && mkdir -p /etc/supervisor.d \
  && mkdir -p /etc/container_start_scripts

COPY config/supervisord.ini.template /etc/supervisor.d/supervisord.ini.template
COPY config/supervisord.conf.template /etc/supervisord.conf.template
COPY docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh
RUN chmod +x /usr/local/bin/docker-entrypoint.sh

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["/usr/bin/supervisord","-n","-c","/etc/supervisord.conf"]

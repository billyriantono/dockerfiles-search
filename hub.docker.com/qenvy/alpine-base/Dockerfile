FROM alpine:3.8

LABEL \
  com.qenvy.vendor="Qenvy" \
  com.qenvy.name="Qenvy Alpine Base Image" \
  com.qenvy.maintainer="Qenvy <info@qenvy.io>" \
  com.qenvy.license="BSD-3-Clause" \
  com.qenvy.version="1.0.0"

ENV LC_ALL=en_US.UTF-8 \
    LANG=en_US.UTF-8 \
    LANGUAGE=en_US.UTF-8 \
    EDITOR=vim \
    QE_PATH=""

RUN set -ex; \
    # installing tools
    apk add --update --upgrade --no-cache \
        findutils \
        bind-tools \
        curl \
        git \
        bash bash-completion \
        vim \
        make \
        supervisor \
    ; \
    # installing mustache (for rendering environment variables)
    curl -sSL https://git.io/get-mo -o mo; chmod +x mo; mv mo /usr/bin/; \
    # configure
    mkdir -p /var/log/supervisor/ /etc/supervisor/conf.d/; \
    # clean up
    rm -rf /etc/apk/cache/* /tmp/* /var/tmp/*

COPY rootfs /

RUN ln -s /opt/utils/entrypoint.sh /usr/local/bin/entrypoint; \
    ln -s /opt/utils/util.sh /usr/local/bin/util

ENTRYPOINT ["entrypoint"]

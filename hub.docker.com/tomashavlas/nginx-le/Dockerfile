FROM tomashavlas/nginx:1.12-debian9

USER 0

ENV CERTBOT_VERSION=0.21 \
    CERTBOT_RELEASE=0.21.1

LABEL name="tomashavlas/nginx-le"

ENV CERTBOT_CONF_PATH=/etc/letsencrypt \
    CERTBOT_LIVE_PATH=/etc/letsencrypt/live \
    CERTBOT_LIB_PATH=/var/lib/letsencrypt \
    CERTBOT_LOG_PATH=/var/log/letsencrypt \
    CERTBOT_WEBROOT_PATH=/srv/letsencrypt

RUN apt-get update \
 && RUNTIME_DEPS=" \
        python \
        python-pip \
        python-setuptools " \
 && apt-get install --yes --no-install-recommends --verbose-versions ${RUNTIME_DEPS} \
 && pip install certbot=="${CERTBOT_RELEASE}" \
 && install --directory --group=0 --mode=0770 --owner=48 \
        "${CERTBOT_CONF_PATH}" \
        "${CERTBOT_LIVE_PATH}" \
        "${CERTBOT_LIB_PATH}" \
        "${CERTBOT_LOG_PATH}" \
        "${CERTBOT_WEBROOT_PATH}" \
 \
 && rm --recursive /var/lib/apt/lists/*

COPY [ "./root", "./${NGINX_VERSION}/root", "/" ]
RUN /usr/lib/container-entrypoint/certbot-setup

VOLUME [ "${CERTBOT_LOG_PATH}" ]

USER 48

CMD [ "/usr/lib/s2i/usage" ]

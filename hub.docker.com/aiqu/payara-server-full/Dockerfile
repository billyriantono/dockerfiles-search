ARG PAYARA_VERSION

FROM payara/server-full:${PAYARA_VERSION:-5.192}

ARG ACTIVEMQ_RAR_VER
ARG JDBC_POSTGRES_VER
ARG JDBC_MSSQL_VER
ARG LOGBACK_VER
ARG SIMPLE_LOG_VER

ENV ACTIVEMQ_RAR_VER=${ACTIVEMQ_RAR_VER:-5.15.9} \
    JDBC_POSTGRES_VER=${JDBC_POSTGRES_VER:-42.2.6} \
    JDBC_MMSQL_VER=${JDBC_MMSQL_VER:-7.2} \
    LOGBACK_VER=${LOGBACK_VER:-1.0.13} \
    SIMPLE_LOG_VER=${SIMPLE_LOG_VER:-1.7.25}

ENV LANG_PREFIX="nb_NO" \
    LANG="nb_NO.ISO-8859-1" \
    LANGUAGE="nb_NO.ISO-8859-1" \
    TZ="Europe/Oslo"

COPY --chown=root:root scripts/*.sh /scripts/

USER root

RUN set -eux && \
    chmod +x /scripts/*.sh && \
    /bin/bash -c '/scripts/initialize.sh' && \
    /bin/bash -c '/scripts/download.sh' && \
    /bin/bash -c '/scripts/add-locales.sh' && \
    /bin/bash -c '/scripts/set-timezone.sh'

USER payara

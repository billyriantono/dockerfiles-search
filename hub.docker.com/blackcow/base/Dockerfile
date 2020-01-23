FROM alpine:3.6
LABEL maintainer="Paul Jefferson <paul.jefferson@blackcow-technology.co.uk>"

RUN apk update && apk add --no-cache \
    bash \
    libpq \
    python \
    tar \
    uwsgi \
    uwsgi-http \
    uwsgi-python \
    vim

ENV APP_USER rgs
ENV APP_GROUP rgs

ENV APP_HOME /opt/oga
ENV APP_VENV ${APP_HOME}/venv
ENV APP_INSTALL_DIR ${APP_HOME}/rgs
ENV LOG_BASE /var/log/oga

EXPOSE 6543

RUN mkdir -p ${APP_HOME} ${APP_INSTALL_DIR}

RUN addgroup ${APP_GROUP}
RUN adduser -S -G ${APP_GROUP} -h ${APP_HOME} -s /sbin/nologin ${APP_USER}

RUN mkdir -p ${LOG_BASE} && \
    chown -R ${APP_USER}:${APP_GROUP} ${APP_HOME} ${LOG_BASE}

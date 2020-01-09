FROM blackcow/base
LABEL maintainer="Paul Jefferson <paul.jefferson@blackcow-technology.co.uk>"

RUN apk update && apk add --no-cache \
    g++ \
    gcc \
    git \
    inotify-tools \
    libffi-dev \
    libxml2-dev \
    libxslt-dev \
    linux-headers \
    postgresql-client \
    postgresql-dev \
    py-virtualenv \
    python-dev

WORKDIR ${APP_INSTALL_DIR}
USER ${APP_USER}

RUN mkdir -p ${APP_VENV} ${APP_INSTALL_DIR} ${APP_HOME}/.cache

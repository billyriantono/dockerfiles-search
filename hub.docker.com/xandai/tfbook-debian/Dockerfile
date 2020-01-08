ARG DATABOOK_DEBIAN_VERSION="1.0.0"

FROM xandai/databook-debian:${DATABOOK_DEBIAN_VERSION}

ARG JUPYTER_USER="jupyter"

ARG TENSORFLOW_VERSION='1.13.1'

USER root

RUN python -m pip install --no-cache-dir tensorflow==${TENSORFLOW_VERSION}

USER ${JUPYTER_USER}

FROM kingrando/net-toolkit-base

RUN set -e -x \
    && set export DEBIAN_FRONTEND=noninteractive \
    && apt-get update \
    && apt-get -y --no-install-recommends install \
        apt-utils \
        libxml2-dev \
        libxslt1-dev \
    && pip3 install pyang \
    && pip3 install ncclient \
    && rm -rf /var/lib/apt/lists/*

VOLUME ["/data"]
CMD [ "sh", "-c", "cd; exec bash -i" ]

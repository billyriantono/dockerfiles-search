FROM getopts/base
MAINTAINER Ming Gao <getopts@163.com>

CMD ["/sbin/my_init", "--", "/bin/bash", "-l"]

RUN add-apt-repository -y ppa:jonathonf/python-3.6 \
    && apt-get update -q \
    && DEBIAN_FRONTEND=noninteractive apt-get install -yq --no-install-recommends \
        python3.6 \
        python3-pip \
    && update-alternatives --install \
        /usr/bin/python3 python3 /usr/bin/python3.5 10 \
    && update-alternatives --install \
        /usr/bin/python3 python3 /usr/bin/python3.6 20 \
    && python3 -V \
    && pip3 install --quiet --no-cache-dir --upgrade pip setuptools wheel \
    && pip3 list --format legacy \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

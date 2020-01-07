# This image is based on "debian:stretch"
FROM postgres:10

RUN set -x \
    && apt-get update && apt-get install -y --no-install-recommends \
        git \
        lzop \
        python3 \
        python3-pip \
        python3-setuptools \
        pv \
    && rm -rf /var/lib/apt/lists/*

RUN python3 -m pip install -U pip \
    && python3 -m pip install --no-cache-dir "git+https://github.com/pjknkda/wal-e.git@v1.1.1b3#egg=wal-e[azure]"

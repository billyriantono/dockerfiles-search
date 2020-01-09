FROM python:3.7-slim-stretch

ENV UNIT_VERSION 1.11.0

RUN apt-get update \
    && apt-get install --no-install-recommends --no-install-suggests -y \
            build-essential curl wget && rm -rf /var/lib/apt/lists/* \
    && cd /tmp && wget -qO - "http://unit.nginx.org/download/unit-$UNIT_VERSION.tar.gz" | tar xvz \
    && cd unit-$UNIT_VERSION \
    && ./configure --prefix=/usr \
                 --modules=lib --control='unix:/var/run/control.unit.sock' \
                 --log=/dev/stdout \
                 --pid=/var/run/unitd.pid \
    && ./configure python --config=/usr/local/bin/python-config \
    && make install \
    && rm -rf /tmp/unit-$UNIT_VERSION \
    && apt-get remove --auto-remove -y build-essential wget

STOPSIGNAL SIGTERM
CMD ["unitd", "--no-daemon", "--control", "unix:/var/run/control.unit.sock"]

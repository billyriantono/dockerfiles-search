FROM debian:jessie
LABEL maintainer="Emanuele Disco <emanuele.disco@gmail.com>"

RUN set -e && \
    mkdir -p /mnt/tmp && \

    # installing required packages
    apt-get update && apt-get install -y \
        openssl \
        git \
        curl

RUN set -e && \
    # installing python 2.x
    apt-get install -y python && \
    #ln -s /usr/bin/python3 /usr/bin/python && \
    # installing pip
    curl https://bootstrap.pypa.io/get-pip.py -o /usr/local/src/get-pip.py && \
    python /usr/local/src/get-pip.py --user && \
    # installing virtualenv
    ~/.local/bin/pip install -U virtualenv

RUN set -e && \
    # installing sphinx
    virtualenv /opt/sphinx && \
    . /opt/sphinx/bin/activate && \
    pip install sphinx && \
    deactivate

RUN set -e && \
    apt-get install -y openjdk-7-jre && \

    # cleaning
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /tmp/* && \
    rm -rf /usr/local/src

WORKDIR /mnt/tmp
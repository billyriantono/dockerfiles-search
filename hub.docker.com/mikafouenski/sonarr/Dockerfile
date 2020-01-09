FROM linuxserver/sonarr
MAINTAINER Mikafouenski

RUN apt update && \
    apt install -y ffmpeg python-pip python-setuptools && \
    pip install \
        requests \
        requests[security] \
        requests-cache \
        babelfish \
        "guessit<2" \
        stevedore==1.19.1 \
        python-dateutil \
        deluge-client \
        qtfaststart


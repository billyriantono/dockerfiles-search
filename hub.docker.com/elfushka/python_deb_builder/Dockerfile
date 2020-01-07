FROM ubuntu:16.04

# install  build dependencies
RUN dpkg --add-architecture i386 \
    && apt-get update \
    && apt-get install -qfy \
        build-essential \
        debhelper \
        devscripts \
        equivs \
        libffi-dev \
        software-properties-common

# install python3.6 build dependencies
RUN add-apt-repository ppa:sebdoido/spotify-dh-virtualenv-stable-1.0 \
    && add-apt-repository ppa:jonathonf/python-3.6 \
    && apt-get -q update \
    && apt-get -qfy install \
        dh-virtualenv \
        python3.6 \
        python3.6-dev \
        python3-pip \
        python3.6-venv

VOLUME /build
WORKDIR /build
COPY entrypoint.sh /usr/local/bin

ENTRYPOINT ["entrypoint.sh"]

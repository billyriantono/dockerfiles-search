FROM python:3.6.5-slim

ENV STAGE 'stage'

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        supervisor \
        wget \
        bash \
        gnupg \
        dirmngr \
        locales \
        gettext-base \
        git \
        mercurial \
        curl \
        gcc \
        sudo \
        python3-dev \
        libmagic-dev \
        calibre \
        locales locales-all \
    && rm -rf /var/lib/apt/lists/*

ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8
RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen \
    && echo "ru_RU.UTF-8 UTF-8" >> /etc/locale.gen \
    && locale-gen \
    && locale -a

RUN groupadd -r selfpub --gid=990 && useradd -r -g selfpub -g sudo --uid=990 -d /app selfpub

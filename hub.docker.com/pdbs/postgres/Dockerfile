FROM ubuntu:latest
LABEL build="201809041140"
LABEL maintainer "marc.jakob@bs.ch"

COPY dpkg-excludes /etc/dpkg/dpkg.cfg.d/excludes
COPY start.sh /

ENV TZ='Europe/Zurich'

RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections && \
    apt-get update && \
    apt-get dist-upgrade -y && \
    apt-get -y install locales && \
    locale-gen en_US.UTF-8 && \
    locale-gen de_CH.UTF-8 && \
    apt-get -y install postgresql && \
    chmod 0750 /start.sh && \
    apt-get autoremove -y && \
    apt-get clean && \
    rm -rf /var/lib/postgresql/*/main /var/lib/apt/lists/*

EXPOSE 5432
ENTRYPOINT ["/start.sh"]
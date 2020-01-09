#FROM ubuntu:14.04
FROM ubuntu:16.04

ENV LANG pt_BR.UTF-8
ENV LANGUAGE pt_BR
ENV LC_CTYPE pt_BR.UTF-8
ENV LC_ALL pt_BR.UTF-8

#COPY config/1404_etc_apt_sources.list /etc/apt/sources.list
COPY config/1604_etc_apt_sources.list /etc/apt/sources.list

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 561F9B9CAC40B2F7

RUN apt-get update \
### Ubuntu
    && apt-get install -y vim curl language-pack-pt locales wget xzdec \
    && rm -rf /var/lib/apt/lists/* \
    && localedef -i pt_BR -c -f UTF-8 -A /usr/share/locale/locale.alias pt_BR.UTF-8 \
    && apt-get update
### Ubuntu

RUN apt-get install -y texlive-full

RUN apt-get update

RUN addgroup --gid 9999 app \
    && adduser --uid 9999 --gid 9999 --disabled-password --gecos "Application" app \
    && usermod -L app \
    && mkdir -p /home/app/.ssh \
    && chmod 700 /home/app/.ssh \
    && chown app:app /home/app/.ssh

RUN apt-get install -y build-essential

USER app
RUN cd /usr/bin
RUN tlmgr init-usertree; exit 0
RUN tlmgr option repository ftp://tug.org/historic/systems/texlive/2015/tlnet-final; exit 0
RUN tlmgr update --self; exit 0
RUN tlmgr install abntex2 selnolig
RUN texhash
USER root

RUN cd /usr/share/texlive/texmf-dist/web2c \
    && sed 's/openout_any\s=\sp/openout_any = a/' texmf.cnf > new_texmf.cnf \
    && mv new_texmf.cnf texmf.cnf

RUN apt-get autoremove -y \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

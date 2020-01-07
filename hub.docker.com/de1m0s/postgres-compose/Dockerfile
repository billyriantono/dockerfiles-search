FROM postgres
MAINTAINER De1mos <de1m0s242@gmail.com>

RUN localedef -i ru_RU -c -f UTF-8 -A /usr/share/locale/locale.alias ru_RU.UTF-8
ENV LANG ru_RU.utf8

COPY russian.affix /usr/share/postgresql/9.5/tsearch_data/russian.affix
COPY russian.dict /usr/share/postgresql/9.5/tsearch_data/russian.dict
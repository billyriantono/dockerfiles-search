# base version targeted from Docker Hub
ARG BASE_VERSION=10.5
# Debian base
FROM postgres:${BASE_VERSION}
# locale
ARG LOCALE_LANG=fr
ARG LOCALE_TERR=FR
ARG LOCALE_CODE=UTF-8
# add locale
RUN localedef -i ${LOCALE_LANG}_${LOCALE_TERR} -c -f ${LOCALE_CODE} -A /usr/share/locale/locale.alias ${LOCALE_LANG}_${LOCALE_TERR}.${LOCALE_CODE}
ENV LANG ${LOCALE_LANG}_${LOCALE_TERR}.${LOCALE_CODE}

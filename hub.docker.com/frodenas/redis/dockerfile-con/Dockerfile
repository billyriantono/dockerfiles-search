FROM alpine:3.4
MAINTAINER Arthur Axel fREW Schmidt <frioux@gmail.com>

RUN \
   apk update && \
   apk add build-base python py-pip python-dev postgresql-dev && \
   pip install pgcli && \
   apk del build-base && \
   rm -rf /root/.cache \
       /usr/lib/python2.7/distutils  \
       /usr/lib/python2.7/idlelib    \
       /usr/lib/python2.7/lib-tk     \
       /usr/lib/python2.7/ensurepip  \
       /usr/lib/python2.7/pydoc_data \
       /var/cache/apk/*

ENTRYPOINT ["pgcli"]

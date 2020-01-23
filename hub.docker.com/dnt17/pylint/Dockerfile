FROM python:3-alpine
MAINTAINER Devin Nathan-Turner <devin@dnt.tech>

ENV PYLINT_VERSION=1.7.4

RUN apk add --no-cache --virtual .run-deps git \
 && pip install pylint==$PYLINT_VERSION \
 && mkdir -p /code

COPY pylint.cfg /etc/pylint.cfg
COPY docker-entrypoint.sh /

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["pylint"]

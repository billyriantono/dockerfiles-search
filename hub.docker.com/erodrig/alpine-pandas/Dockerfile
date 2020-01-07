FROM python:3.6-alpine

MAINTAINER Eduardo Rodriguez<sinapsis490@gmail.com>

#Application dependencies
ENV SO_PACKAGES="\
    tzdata \
"

ENV PYTHON_BASICS="\
    pandas==0.23.4\
"

RUN set -ex \
	&& apk add --no-cache --update $SO_PACKAGES \
    && apk add --no-cache --virtual .build-deps \
            g++ \
    && python3.6 -m venv /venv \
    && /bin/sh -c "/venv/bin/pip install --upgrade pip setuptools" \
    && LIBRARY_PATH=/lib:/usr/lib /bin/sh -c "/venv/bin/pip install --no-cache-dir $PYTHON_BASICS" \
    && runDeps="$( \
            scanelf --needed --nobanner --recursive /venv \
                    | awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' \
                    | sort -u \
                    | xargs -r apk info --installed \
                    | sort -u \
    )" \
    && apk add --virtual .python-rundeps $runDeps \
    && apk del .build-deps \
    && echo "Iceland" >  /etc/timezone \
    && cp /usr/share/zoneinfo/Iceland /etc/localtime \
    && apk del tzdata

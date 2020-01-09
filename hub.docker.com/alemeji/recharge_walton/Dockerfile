FROM python:3.6.6-alpine3.8
#python:3.6.6-alpine3.8
#python:3.6-alpine3.8
#python:3.6.5-alpine3.7

ENV DJANGO_ENV=local

ENV PYTHONUNBUFFERED=1

ENV WEBAPP_DIR=/webapp

RUN apk add --update --no-cache mariadb-connector-c-dev mariadb-connector-c \
# RUN apk add --update --no-cache mariadb-client-libs \
	&& apk add --update --no-cache gettext \
	&& apk add --no-cache --virtual .build-deps \
	# mariadb-dev \
    ca-certificates \
    gcc \
    linux-headers \
    # gettext-dev \
    musl-dev \
    libffi-dev \
    jpeg-dev \
    zlib-dev \
	&& pip install --upgrade pip \
	&& pip install mysqlclient==1.3.12 \
    && find /usr/local \
        \( -type d -a -name test -o -name tests \) \
        -o \( -type f -a -name '*.pyc' -o -name '*.pyo' \) \
        -exec rm -rf '{}' + \
    && runDeps="$( \
        scanelf --needed --nobanner --recursive /usr/local \
                | awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' \
                | sort -u \
                | xargs -r apk info --installed \
                | sort -u \
    )" \
    && apk add --virtual .rundeps $runDeps \
	&& apk del .build-deps \
	&& mkdir $WEBAPP_DIR \
	&& mkdir -p /var/log/gunicorn


# RUN apk add --update --no-cache mariadb-client-libs \
# 	&& apk add --no-cache --virtual .build-deps \
# 		mariadb-dev \
# 		gcc \
# 		musl-dev \
# 	&& pip install --upgrade pip \
# 	&& pip install mysqlclient==1.3.12 \
# 	&& apk del .build-deps \
# 	&& mkdir $WEBAPP_DIR \
# 	&& mkdir -p /var/log/gunicorn

WORKDIR $WEBAPP_DIR

# ADD requirements.txt $WEBAPP_DIR/
ADD requirements/base.txt $WEBAPP_DIR/
ADD requirements/$DJANGO_ENV.txt $WEBAPP_DIR/

# RUN pip install -r requirements.txt
RUN pip install -r $DJANGO_ENV.txt \
    && find /usr/local \
        \( -type d -a -name test -o -name tests \) \
        -o \( -type f -a -name '*.pyc' -o -name '*.pyo' \) \
        -exec rm -rf '{}' + \
    && runDeps="$( \
        scanelf --needed --nobanner --recursive /usr/local \
                | awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' \
                | sort -u \
                | xargs -r apk info --installed \
                | sort -u \
    )" \
    && apk add --virtual .rundeps $runDeps

ADD . $WEBAPP_DIR/

RUN export DJANGO_SETTINGS_MODULE= \
    && django-admin.py makemessages -l es \
    && django-admin.py compilemessages

EXPOSE 8000


FROM python:3.6-alpine3.6
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/' /etc/apk/repositories && apk update

ARG VERSION=master

RUN set -xe \
 && apk add --no-cache tiff-dev jpeg-dev zlib-dev freetype-dev lcms-dev libwebp-dev tcl-dev tk-dev \
        python3-dev libressl-dev openldap-dev cyrus-sasl-dev krb5-dev sshpass postgresql-dev \
        mariadb-dev sqlite-dev libffi-dev openssh-client

WORKDIR /app/jumpserver

ADD requirements.txt .

RUN set -xe \
 && apk add --no-cache --virtual .build-deps build-base \
 && pip install -i https://mirrors.aliyun.com/pypi/simple/ -r requirements.txt \
    psycopg2 \
 && apk del .build-deps

RUN set -xe \
 && apk add curl bash \
 && curl -sSL -o - https://github.com/jumpserver/jumpserver/archive/${VERSION}.tar.gz | tar zxf - \
 && mv jumpserver-${VERSION}/* /app/jumpserver \
 && rm -rf jumpserver-${VERSION}

ADD config.py .

VOLUME /app/jumpserver/data
VOLUME /app/jumpserver/logs

EXPOSE 8080
CMD ["./entrypoint.sh"]

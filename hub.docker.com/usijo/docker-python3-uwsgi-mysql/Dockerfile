FROM usijo/docker-python3
MAINTAINER Hongshun Yang <ojisucom@gmail.com>

RUN apk add -U libxml2 mariadb-client-libs
RUN apk add -U --virtual build-deps python3-dev build-base zlib-dev jpeg-dev \ 
libffi-dev openssl-dev libxslt-dev libxml2-dev freetype-dev linux-headers mariadb-dev \
&& ln -s /usr/include/locale.h /usr/include/xlocale.h \
&& pip install virtualenv uwsgi mysqlclient \
&& apk del -U --purge build-deps 



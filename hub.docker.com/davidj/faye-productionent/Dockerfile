FROM python:2.7-stretch

RUN DEPS_BUILD="wget sudo python-setuptools python-dev build-essential libssl-dev libxml2-dev libxslt1-dev libbz2-dev libjpeg62-turbo-dev libtiff5-dev libopenjp2-7-dev" \
    DEPS_RUN="libxml2 libxslt1.1 libjpeg62 rsync lynx wv libtiff5 libopenjp2-7 poppler-utils" \
    && apt-get update \
    && apt-get install -y --no-install-recommends $DEPS_BUILD \
    && apt-get install -y --no-install-recommends $DEPS_RUN \
    libcurl3-dev \
    libfreetype6 \
    libfreetype6-dev \
    imagemagick

RUN apt-get install -y python3-dev python2.7-dev libldap2-dev libsasl2-dev ldap-utils python-tox lcov valgrind

COPY requirements.txt ./
COPY constraints.txt ./

RUN pip install -r requirements.txt -c constraints.txt Plone

FROM ubuntu:14.04.2
MAINTAINER Jason Kraus "jason@montagable.com"
RUN apt-get -qq update
RUN apt-get install -y python-dev python-setuptools libxml2-dev libxslt-dev libmysqlclient-dev postgresql-client libpq-dev git-core wget make g++ libjpeg-dev libfreetype6 libfreetype6-dev zlib1g-dev curl libevent-dev libmemcached-dev libyaml-dev python-mysqldb gettext phantomjs libffi-dev
RUN curl -sL https://deb.nodesource.com/setup_0.12 | bash -
RUN apt-get install -y nodejs
RUN apt-get -yqq clean
RUN easy_install pip
RUN pip install pyopenssl ndg-httpsclient pyasn1
RUN npm install -g gulp less babel

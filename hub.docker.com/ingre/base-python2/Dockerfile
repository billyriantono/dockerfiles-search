FROM python:2.7.9

MAINTAINER Marek Wywiał <marek.wywial@ingre.pl>

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && \
    apt-get -yq install \
    libpq-dev libxml2-dev libxslt1-dev libjpeg62-turbo libjpeg-dev \
    libfreetype6-dev tcl-dev tk-dev libpng12-dev \
    libyaml-dev python-yaml locales unzip supervisor cron \
    postgresql-client-9.4 vim rsyslog git

ADD rsyslog.conf /etc/rsyslog.conf


RUN apt-get clean
RUN echo 'pl_PL.UTF-8 UTF-8' >> /etc/locale.gen
RUN locale-gen
ENV LANG pl_PL.UTF_8
ENV LANGUAGE pl_PL:pl
ENV LC_ALL pl_PL.UTF-8

# upgrade/install base pip packages
RUN pip install --upgrade pip
RUN pip install --upgrade fabric distribute setuptools uwsgi psycopg2 supervisor-stdout

CMD ["python2"]

FROM redbadger/base:latest

RUN groupadd -r postgres && useradd -r -g postgres postgres

RUN \
  apt-key adv --keyserver keyserver.ubuntu.com --recv-keys B97B0AFCAA1A47F044F244A07FCC7D46ACCC4CF8 &&\
  echo "deb http://apt.postgresql.org/pub/repos/apt/ trusty-pgdg main 9.3" > /etc/apt/sources.list.d/pgdg.list &&\
  apt-get update

RUN \
  DEBIAN_FRONTEND=noninteractive apt-get -y install language-pack-en &&\
  export LANGUAGE=en_US.UTF-8 &&\
  export LANG=en_US.UTF-8 &&\
  export LC_ALL=en_US.UTF-8 &&\
  DEBIAN_FRONTEND=noninteractive locale-gen en_US.UTF-8 &&\
  DEBIAN_FRONTEND=noninteractive dpkg-reconfigure locales &&\
  update-locale LANG=en_US.UTF-8

RUN \
  LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8 DEBIAN_FRONTEND=noninteractive apt-get install -y \
  libpq5 \
  postgresql-9.3 \
  postgresql-client-9.3 \
  postgresql-contrib-9.3

ENV PATH /usr/lib/postgresql/9.3/bin:$PATH
RUN mkdir /data
VOLUME /data
ENV PGDATA /data

EXPOSE 5432
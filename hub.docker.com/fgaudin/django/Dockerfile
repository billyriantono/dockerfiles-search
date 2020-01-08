FROM fgaudin/base:3
MAINTAINER Francois Gaudin <francois@presencelearning.com>

RUN \
  apt-get update && apt-get install -y build-essential python-dev python-pip openssl libxml2-dev libxslt1-dev \
  zlib1g-dev python-mysqldb libevent-dev libmagickwand-dev

RUN groupadd django -g 108000 && useradd django -u 108000 -p $(openssl passwd -1 "django")  -d /opt/app -s /bin/bash -g 108000 -g sudo

COPY start.sh /opt/start.sh

RUN chmod +x /opt/start.sh

VOLUME ["/opt/app"]

WORKDIR /opt/app

EXPOSE 8000

CMD ["/opt/start.sh"]
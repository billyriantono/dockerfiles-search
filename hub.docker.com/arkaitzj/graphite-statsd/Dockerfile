#mb
FROM debian
MAINTAINER Arkaitz Jimenez arkaitzj@gmail.com

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y build-essential sudo vim net-tools pkg-config python-pip curl procps
RUN pip install --upgrade pip

RUN apt-get update && apt-get install -y supervisor memcached python-dev libcairo2 libcairo2-dev python-cairo sqlite3  git

RUN git clone https://github.com/joyent/node.git && cd node && git checkout v0.11.11 && ./configure --openssl-libpath=/usr/lib/ssl && make && make install && cd .. && rm -rf node
RUN mkdir -p /opt && git clone https://github.com/etsy/statsd /opt/statsd && cd /opt/statsd && git checkout v0.7.1 && cp exampleConfig.js local.js

ADD initial_data.json /opt/graphite/webapp/graphite/initial_data.json
ADD dependencies.txt /opt/graphite/
RUN pip install -r /opt/graphite/dependencies.txt

RUN mkdir -p /opt/graphite/storage/log/webapp

ADD storage-schemas.conf /opt/graphite/conf/
ADD carbon.conf /opt/graphite/conf/
ADD local_settings.py /opt/graphite/webapp/graphite/
ADD config.js /opt/statsd/

RUN mkdir -p /opt/graphite/storage/whisper

RUN python /opt/graphite/webapp/graphite/manage.py syncdb --noinput
RUN chown -R www-data.www-data /opt/graphite

ADD supervisord.conf /etc/supervisor/conf.d/

CMD ["/usr/bin/supervisord"]

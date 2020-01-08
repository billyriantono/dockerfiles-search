FROM ubuntu:18.04 as base

ENV TZ=Europe/Vilnius
ENV DEBIAN_FRONTEND noninteractive

ENV GRAPHITE_VERSION=1.1.5 \
    STATSD_VERSION=v0.8.5 \
    TWISTED_VERSION=13.2.0 \
    GRAFANA_VERSION=6.2.5

RUN apt-get update -q && apt-get -q -y install supervisor software-properties-common \
	git python-django-tagging python-simplejson python-memcache python-ldap python-cairo python-pysqlite2 python-pip python-dev \
	wget nginx curl build-essential gunicorn

RUN mkdir -p /var/log/supervisor

RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -
RUN apt-get install -y nodejs

RUN     pip install Twisted==$TWISTED_VERSION \
        && pip install pytz

RUN mkdir -p /src \
		&& git clone https://github.com/graphite-project/whisper.git /src/whisper \
		&& cd /src/whisper \
		&& git checkout $GRAPHITE_VERSION \
		&& python setup.py install

RUN git clone https://github.com/graphite-project/carbon.git /src/carbon \
		&& cd /src/carbon \
		&& git checkout $GRAPHITE_VERSION \
		&& python setup.py install

RUN git clone https://github.com/graphite-project/graphite-web.git /src/graphite-web \
		&& cd /src/graphite-web \
		&& git checkout $GRAPHITE_VERSION \
		&& python setup.py install \
		&& pip install -r requirements.txt \
		&& python check-dependencies.py

RUN git clone https://github.com/etsy/statsd.git /src/statsd \
		&& cd /src/statsd \
		&& git checkout $STATSD_VERSION

RUN mkdir /src/grafana \
		&& mkdir /opt/grafana \
		&& wget https://dl.grafana.com/oss/release/grafana-${GRAFANA_VERSION}.linux-amd64.tar.gz -O /src/grafana.tar.gz \
		&& tar -xzf /src/grafana.tar.gz -C /opt/grafana --strip-components=1 \
		&& rm /src/grafana.tar.gz

ADD ./config/statsd/config.js /src/statsd/config.js

ADD ./config/graphite/carbon.conf /opt/graphite/conf/carbon.conf
ADD ./config/graphite/initial_data.json /opt/graphite/webapp/graphite/initial_data.json
ADD ./config/graphite/local_settings.py /opt/graphite/webapp/graphite/local_settings.py
ADD ./config/graphite/storage-schemas.conf /opt/graphite/conf/storage-schemas.conf
ADD ./config/graphite/storage-aggregation.conf /opt/graphite/conf/storage-aggregation.conf

RUN mkdir -p /opt/graphite/storage/whisper \
		&& touch /opt/graphite/storage/graphite.db /opt/graphite/storage/index \
		&& chown -R www-data /opt/graphite/storage \
		&& chmod 0775 /opt/graphite/storage /opt/graphite/storage/whisper \
		&& chmod 0664 /opt/graphite/storage/graphite.db \
		&& cp /src/graphite-web/webapp/manage.py /opt/graphite/webapp \
		&& cd /opt/graphite/webapp/ \
		&& python manage.py migrate --run-syncdb --noinput

ADD ./config/grafana/custom.ini /opt/grafana/conf/custom.ini

RUN mkdir /src/datasources \
		&& mkdir /src/dashboards

# Configure nginx and supervisord
ADD     ./config/nginx/nginx.conf /etc/nginx/nginx.conf
ADD     ./config/supervisor/supervisord.conf /etc/supervisor/conf.d/supervisord.conf
# Grafana
EXPOSE  80
# Graphite
EXPOSE 2003
# StatsD UDP port
EXPOSE  8125/udp
# StatsD Management port
EXPOSE  8126

CMD     ["/usr/bin/supervisord"]
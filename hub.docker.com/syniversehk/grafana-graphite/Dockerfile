FROM 	centos:centos6

RUN rpm -Uvh http://download.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm

# ---------------- #
#   Installation   #
# ---------------- #

# Install required packages
RUN yum -y install gcc python-devel pycairo python-pip python-django-tagging \
     python-simplejson python-gunicorn supervisor nginx git wget tar nodejs \
     bitmap bitmap-fonts

# Use pip to install graphite, carbon, and deps
RUN pip install whisper Twisted==11.1.0 carbon graphite-web

# Checkout the stable branches of Graphite, Carbon and Whisper and install from there
RUN     mkdir /src

# Install StatsD
RUN     git clone https://github.com/etsy/statsd.git /src/statsd                                                                        &&\
        cd /src/statsd                                                                                                                  &&\
        git checkout v0.8.0

# Install Grafana
RUN     mkdir /opt/grafana                                                                                    &&\
        wget https://grafanarel.s3.amazonaws.com/builds/grafana-3.1.1-1470047149.linux-x64.tar.gz -O /src/grafana.tar.gz &&\
        tar -xzf /src/grafana.tar.gz -C /opt/grafana --strip-components=1                                     &&\
        rm /src/grafana.tar.gz

# ----------------- #
#   Configuration   #
# ----------------- #

# Confiure StatsD
ADD     ./statsd/config.js /src/statsd/config.js

# Configure Whisper, Carbon and Graphite-Web
ADD     ./graphite/initial_data.json /opt/graphite/webapp/graphite/initial_data.json
ADD     ./graphite/local_settings.py /opt/graphite/webapp/graphite/local_settings.py
ADD     ./graphite/carbon.conf /opt/graphite/conf/carbon.conf
ADD     ./graphite/storage-schemas.conf /opt/graphite/conf/storage-schemas.conf
ADD     ./graphite/storage-aggregation.conf /opt/graphite/conf/storage-aggregation.conf

RUN     mkdir -p /opt/graphite/storage/whisper                                                                 &&\
     touch /opt/graphite/storage/graphite.db /opt/graphite/storage/index                                       &&\
     chown -R nobody /opt/graphite/storage                                                                     &&\
     chmod 0775 /opt/graphite/storage /opt/graphite/storage/whisper                                            &&\
     chmod 0664 /opt/graphite/storage/graphite.db                                                              &&\
     cd /opt/graphite/webapp/graphite && python manage.py syncdb --noinput

# Configure Grafana
ADD     ./grafana/custom.ini /opt/grafana/conf/custom.ini

# Add the default dashboards
RUN     mkdir /src/dashboards
ADD     ./grafana/dashboards/* /src/dashboards/

# Configure nginx and supervisord
ADD     ./nginx/nginx.conf /etc/nginx/nginx.conf
ADD     ./supervisord.conf /etc/supervisord.conf

# ---------------- #
#   Expose Ports   #
# ---------------- #

# Grafana
EXPOSE  80

# StatsD UDP port
EXPOSE  8125/udp

# StatsD Management port
EXPOSE  8126

# Graphite web port
EXPOSE 81
EXPOSE 2003
EXPOSE 2004

# -------- #
#   Run!   #
# -------- #

CMD     ["/usr/bin/supervisord"]

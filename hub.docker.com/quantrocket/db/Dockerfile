FROM quantrocket/anaconda3-uwsgi
MAINTAINER QuantRocket <support@quantrocket.com>

COPY uwsgi /etc/uwsgi/
COPY qrocket /tmp/uwsgi/qrocket

RUN mkdir -p /tmp/s3/staging \
  && mkdir -p /var/tmp/uwsgi/mule \
  && /tmp/build.sh

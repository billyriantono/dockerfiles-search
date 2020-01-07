FROM quantrocket/anaconda3-uwsgi
MAINTAINER QuantRocket <support@quantrocket.com>

ENV IBG_CLIENT_RANGE=7000 UWSGI_WORKERS=3 UWSGI_CACHE2_BLOCKSIZE=131072
COPY qrocket /tmp/uwsgi/qrocket
COPY uwsgi /etc/uwsgi

RUN mkdir -p /tmp/realtime \
  && mkdir -p /var/tmp/uwsgi/spool \
  && /tmp/build.sh

CMD ["uwsgi-quantrocket", "--emperor", "/etc/uwsgi/uwsgi*.ini"]

FROM pataquets/collectd-python

ADD \
  https://raw.githubusercontent.com/powdahound/redis-collectd-plugin/master/redis_info.py \
  /opt/collectd/lib/collectd/plugins/python/

ADD \
  https://raw.githubusercontent.com/powdahound/redis-collectd-plugin/master/redis.conf \
  /etc/collectd/conf.d/

RUN \
  sed -i 's/#Cluster false/Cluster false/' /etc/collectd/conf.d/redis.conf && \
  sed -i 's/Host "localhost"/Host "redis"/' /etc/collectd/conf.d/redis.conf && \
  nl /etc/collectd/conf.d/redis.conf

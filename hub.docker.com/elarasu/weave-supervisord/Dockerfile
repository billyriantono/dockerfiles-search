# supervisord base image
#   docker build -t elarasu/weave-supervisord .
#
FROM elarasu/weave-ubuntu
MAINTAINER elarasu@outlook.com

# supervisord server
RUN  apt-get update \
  && apt-get install -yq supervisor --no-install-recommends \
  && mkdir -p /var/log/supervisor \
  && mkdir -p /etc/supervisor/conf.d/ \
  && rm -rf /tmp/* /var/tmp/* /var/lib/apt/lists/* 

# Add supervisord configuration
ADD conf/supervisord.conf /etc/supervisor/

CMD ["supervisord"]


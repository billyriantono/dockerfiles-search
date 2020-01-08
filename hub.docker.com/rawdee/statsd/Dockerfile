FROM rawdee/nodejs
MAINTAINER Rodolphe Blancho

RUN cd /opt && \
  curl -L https://github.com/etsy/statsd/archive/v0.7.1.tar.gz | tar zx && \
  ln -s statsd-0.7.1 statsd

ADD config.js /opt/statsd/config.js

EXPOSE 8125/udp
EXPOSE 8126

CMD ["node", "/opt/statsd/stats.js", "/opt/statsd/config.js"]

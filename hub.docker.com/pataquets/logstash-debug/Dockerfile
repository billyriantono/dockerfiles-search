FROM pataquets/logstash:2

RUN \
  ln -vs \
    /etc/logstash/conf-available/input-30-tcp.conf \
    /etc/logstash/conf-available/input-50-stdin.conf \
    /etc/logstash/conf-available/output-20-stdout.conf \
    /etc/logstash/conf.d/ \
  && \
  ls -Al /etc/logstash/conf.d/ && \
  cat /etc/logstash/conf.d/*.conf | nl

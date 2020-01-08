FROM logstash

MAINTAINER Alexandre Mioranza <amioranza@mdcnet.ninja>

RUN mkdir -p /etc/logstash/patterns \
    && mkdir -p /etc/logstash/conf.d

COPY logstash.conf /etc/logstash/conf.d/logstash.conf

CMD ["-f", "/etc/logstash/conf.d"]

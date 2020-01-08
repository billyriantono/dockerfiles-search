FROM logstash

COPY logstash.conf /etc/logstash/conf.d/

RUN logstash-plugin install logstash-input-beats

VOLUME /etc/logstash
VOLUME /var/lib/logstash
VOLUME /var/log/logstash

EXPOSE 5044

CMD ["-f", "/etc/logstash/conf.d/logstash.conf"]
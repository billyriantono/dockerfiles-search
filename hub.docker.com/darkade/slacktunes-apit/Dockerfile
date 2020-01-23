FROM logstash:2.3

COPY logstash.conf /etc/logstash/logstash.conf

CMD ["logstash","-f","/etc/logstash/logstash.conf","--allow-env"]

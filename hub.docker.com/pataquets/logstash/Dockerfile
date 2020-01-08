FROM logstash:2

ADD ./files/etc/logstash/ /etc/logstash/

CMD [ "--config", "/etc/logstash/*.conf", "--config", "/etc/logstash/conf.d/" ]

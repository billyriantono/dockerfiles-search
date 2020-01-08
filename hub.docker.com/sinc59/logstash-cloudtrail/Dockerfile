FROM logstash:2.4

RUN /opt/logstash/bin/logstash-plugin install logstash-input-s3
RUN /opt/logstash/bin/logstash-plugin install logstash-codec-cloudtrail
RUN /opt/logstash/bin/logstash-plugin install logstash-output-stdout

COPY cloudtrail.conf /etc/logstash/conf.d/cloudtrail.conf
ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["-e", ""]

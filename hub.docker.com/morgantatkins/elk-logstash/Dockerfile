FROM docker.elastic.co/logstash/logstash:6.4.2
COPY logstash.conf /usr/share/logstash/config/logstash.conf
COPY logstash.yml /usr/share/logstash/config/logstash.yml
COPY template.json /etc/logstash/template.json
USER root
RUN chown logstash /usr/share/logstash/config/logstash.conf && \
    chown logstash /usr/share/logstash/config/logstash.yml && \
    chmod -R +rw /usr/share/logstash/config/
RUN rm -rf /usr/share/logstash/config/logstash-sample.conf
RUN /usr/share/logstash/bin/logstash-plugin install logstash-output-amazon_es
USER logstash
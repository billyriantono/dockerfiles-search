FROM openjdk:8-jre
RUN wget https://artifacts.elastic.co/downloads/logstash/logstash-6.3.2.tar.gz && tar -xzvf logstash-6.3.2.tar.gz
RUN logstash-6.3.2/bin/logstash-plugin install logstash-output-amazon_es
VOLUME  [ "/config" ]
ADD run run
CMD ["run/run.sh"]
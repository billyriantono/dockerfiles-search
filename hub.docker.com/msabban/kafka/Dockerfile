FROM openjdk:8-jre

ENV KAFKA_RELEASE_FILENAME="kafka_2.12-1.0.0"
ENV KAFKA_RELEASE_VERSION="1.0.0"
ENV TOPICS="local0.raw local1.raw local2.raw local3.raw local4.raw local5.raw local6.raw local7.raw apache.parsed auth.parsed ban_distrib.parsed bucket.ban bucket.notification cron.parsed kernel.parsed nginx.parsed rsyslog.parsed ssh.parsed suhosin.parsed unparsed"

RUN apt-get update && apt-get install -y netcat paxctl supervisor
RUN wget http://mirrors.ircam.fr/pub/apache/kafka/$KAFKA_RELEASE_VERSION/$KAFKA_RELEASE_FILENAME.tgz -O $KAFKA_RELEASE_FILENAME.tgz
RUN tar zxvf $KAFKA_RELEASE_FILENAME.tgz -C /
RUN mv /$KAFKA_RELEASE_FILENAME /kafka
RUN paxctl -cspermx $(which java)


EXPOSE 2181

# RUN supervisord -c /etc/supervisor/supervisord.conf &&  until echo test | nc 127.0.0.1 2181; do sleep 0.1; done  && until echo test | nc 127.0.0.1 9092; do sleep 0.1; done && for i in $TOPICS; do /kafka/bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic $i ; done

# RUN supervisorctl shutdown

CMD nc -l -p 10000 && cat $CI_PROJECT_DIR/hosts > /etc/hosts ; rm -rf /tmp/zookeeper && /kafka/bin/zookeeper-server-start.sh /kafka/config/zookeeper.properties
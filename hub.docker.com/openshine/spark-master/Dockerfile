FROM openshine/spark-base:latest
MAINTAINER Roberto Majadas <roberto.majadas@openshine.com>

COPY start.sh /usr/local/bin/

ENV SPARK_RECOVERY_DIR /data/spark-master

EXPOSE 8080/tcp 7077/tcp

CMD ["start.sh"]

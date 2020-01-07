FROM p7hb/docker-spark:2.2.0
MAINTAINER Sunile Manjee <sunilemanjee@gmail.com>

EXPOSE 4040 8080 8081

RUN wget https://s3.amazonaws.com/kinetica-se/Docker-GPU/run_forever.sh -P /usr/local/bin

RUN chmod +x /usr/local/bin/run_forever.sh
RUN wget https://s3.amazonaws.com/kinetica-se/Spark-Connector/v1.0/6.1.0/spark-2.2.0-kinetica-6.1.0-connector.jar -P /root
CMD ["/usr/local/bin/run_forever.sh"]

FROM openjdk:8-jre

RUN curl https://s3.amazonaws.com/nomad-spark/spark-2.2.0-bin-nomad-0.7.0.tgz | tar -xzC /tmp
RUN mv /tmp/spark* /opt/spark

ENV SPARK_HOME /opt/spark
ENV PATH $PATH:$SPARK_HOME/bin
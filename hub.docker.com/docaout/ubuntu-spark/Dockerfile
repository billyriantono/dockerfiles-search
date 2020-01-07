FROM docaout/ubuntu-openjdk:latest

RUN apt-get update && \
    apt-get dist-upgrade -y && \
    apt-get install -y --no-install-recommends curl && \
    curl http://d3kbcqa49mib13.cloudfront.net/spark-2.0.1-bin-hadoop2.7.tgz | tar -xzC /opt && mv /opt/spark* /opt/spark && \
    apt-get autoremove -y && apt-get clean && \
    rm -rf /var/lib/apt/lists/*

ENV SPARK_HOME /opt/spark
ENV PATH ${SPARK_HOME}/bin:$PATH

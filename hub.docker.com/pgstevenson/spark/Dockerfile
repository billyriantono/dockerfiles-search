FROM mcr.microsoft.com/java/jdk:8u232-zulu-ubuntu
MAINTAINER Paul Stevenson <paul@pgstevenson.com>

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y curl \
      git

# Install Scala

RUN curl -O https://downloads.lightbend.com/scala/2.13.1/scala-2.13.1.tgz && \
    tar xvf scala-2.13.1.tgz && \
    mv scala-2.13.1 /usr/local/scala

# Install Spark

RUN curl -O https://archive.apache.org/dist/spark/spark-2.4.4/spark-2.4.4-bin-hadoop2.7.tgz && \
    tar xvf spark-2.4.4-bin-hadoop2.7.tgz && \
    mv spark-2.4.4-bin-hadoop2.7 /usr/local/spark

# Environment Variables

ENV PATH="/usr/local/scala/bin:${PATH}"
ENV PATH="/usr/local/spark/bin:${PATH}"

CMD ["/bin/bash"]

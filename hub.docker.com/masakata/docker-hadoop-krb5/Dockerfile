FROM ubuntu:16.04

ARG CDH_VERSION=5.15.0

# Prerequisites including Kerberos client
RUN apt-get update && \
      apt-get install -y --no-install-recommends \
      ca-certificates \
      gnupg-curl \
      krb5-user \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

# Hadoop client
RUN apt-key adv --fetch-keys https://archive.cloudera.com/cdh5/ubuntu/xenial/amd64/cdh/archive.key \
      && echo deb [arch=amd64] http://archive.cloudera.com/cdh5/ubuntu/xenial/amd64/cdh xenial-cdh$CDH_VERSION contrib | tee -a /etc/apt/sources.list.d/cloudera.list \
      && echo deb [arch=amd64] http://archive.cloudera.com/cm5/ubuntu/xenial/amd64/cm xenial-cm$CDH_VERSION contrib | tee -a /etc/apt/sources.list.d/cloudera.list \
      && echo deb-src http://archive.cloudera.com/cm5/ubuntu/xenial/amd64/cm xenial-cm$CDH_VERSION contrib | tee -a /etc/apt/sources.list.d/cloudera.list

RUN apt-get update && \
      apt-get install -y --no-install-recommends \
              hadoop-client \
              libhdfs0 \
              libhdfs0-dev \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

# Link slf4j-simple.jar
RUN ln -s /usr/share/java/slf4j-simple.jar /usr/lib/hadoop/lib/slf4j-simple.jar

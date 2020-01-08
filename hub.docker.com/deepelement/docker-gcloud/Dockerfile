FROM ubuntu:14.04
MAINTAINER Todd Morrison <todd@deepelement.com>

ENV LC_ALL=C.UTF-8
ENV LANG=C.UTF-8

# Setup Aptitude
RUN apt-key update && \
    apt-get clean && \
    apt-get -y update && \
    apt-get -y upgrade && \
    apt-get -y update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --force-yes \
        software-properties-common \
        python-software-properties \
        2>/dev/null && \
    apt-get -y update

# Install Common Devtools
RUN apt-get -y install \
      build-essential \
      ntp \
      curl \
      zip \
      git  && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* \
    rm -rf /var/cache/apt/*

# Install Java8
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
  add-apt-repository -y ppa:webupd8team/java && \
  apt-get update && \
  apt-get install -y oracle-java8-installer && \
  rm -rf /var/lib/apt/lists/* && \
  rm -rf /var/cache/oracle-jdk8-installer
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

# Install Python3
RUN  apt-add-repository universe -y && \
    apt-get -y update && \
    apt-get -y install \
      python-pip \
      python-dev \
      python3-pip && \
    rm -rf /usr/bin/python && ln -s /usr/bin/python3.4 /usr/bin/python

# Google Cloud SDK install
ENV PATH $PATH:/root/google-cloud-sdk/bin
RUN curl -sSL https://sdk.cloud.google.com | bash && \
    gcloud components update --version 189.0.0 2>/dev/null && \
    gcloud components install \
        bq \
        core \
        gsutil \
        app-engine-go \
        cbt \
        bigtable \
        datalab \
        cloud-datastore-emulator \
        gcd-emulator \
        pubsub-emulator \
        emulator-reverse-proxy \
        container-builder-local \
        alpha \
        beta \
        app-engine-java \
        app-engine-php \
        app-engine-python \
        app-engine-python-extras \
        kubectl

# Setup for ssh for github.com
RUN mkdir -p /root/.ssh
RUN echo "Host github.com\n\tStrictHostKeyChecking no\n" >> /root/.ssh/config
RUN echo -e "machine github.com\n  login 344acd8012eefe9734429d5314bfc78a93e6af6c" >> ~/.netrc


# Setup NodeJS
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - && \
    apt-get install -y nodejs

# Setup Hadoop and HBase
RUN sudo wget 'https://archive.cloudera.com/cdh5/ubuntu/trusty/amd64/cdh/cloudera.list' \ 
        -O /etc/apt/sources.list.d/cloudera.list && \
    curl -s http://archive.cloudera.com/debian/archive.key | \
        apt-key add - && \
    apt-get update && \
    apt-get install hbase -y
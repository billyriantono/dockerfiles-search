FROM debian:stable

LABEL maintainer="myugan59@gmail.com"
LABEL version="6.4.2"

ENV DEBIAN_FRONTEND=noninteractive
ENV ELASTICSEARCH_IP="localhost"
ENV JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64"

# Install general package
RUN apt-get update && apt-get -y upgrade
RUN apt-get -y install software-properties-common apt-transport-https sudo git nano curl wget net-tools gnupg gnupg2

# Install java
RUN echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | debconf-set-selections
RUN echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" > /etc/apt/sources.list.d/webupd8team-java-trusty.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EEA14886
RUN apt-get update && apt-get install -y --force-yes --no-install-recommends oracle-java8-installer && apt-get clean all

# Add elastic repository
RUN echo "deb https://artifacts.elastic.co/packages/6.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-6.x.list
RUN apt-get update

# Install logstash
RUN apt-get -y --allow-unauthenticated install logstash
ADD conf.d /etc/logstash/conf.d/
ADD logstash.yml /etc/logstash/logstash.yml

ADD ./entrypoint.sh /
RUN chmod +x /entrypoint.sh

EXPOSE 5044
ENTRYPOINT [ "/bin/bash" , "/entrypoint.sh"]
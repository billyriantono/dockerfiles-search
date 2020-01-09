FROM maven:3.5.0-jdk-8
MAINTAINER Tokazio, https://github.com/tokazio

# SSH
RUN mkdir -p /root/.ssh
ADD known_hosts /root/.ssh/
ADD id_rsa /root/.ssh/
RUN chmod 700 /root/.ssh/id_rsa

#
RUN mkdir -p /home/docker

#MicroCore
RUN git clone git@bitbucket.org:netesyomicro/microcore.git /home/docker/microcore
RUN mvn install -f /home/docker/microcore/pom.xml

#MicroRegistry
RUN git clone git@bitbucket.org:netesyomicro/microregistry.git /home/docker/microregistry
RUN mvn compile package -f /home/docker/microregistry/pom.xml

#
COPY deploy.sh /home/docker 
RUN chmod 777 /home/docker/deploy.sh

#hazelcast ports
EXPOSE 5702

EXPOSE 8081

VOLUME /root/.m2/repository/
VOLUME /home/docker/log

ENTRYPOINT /home/docker/deploy.sh
WORKDIR /home/docker/

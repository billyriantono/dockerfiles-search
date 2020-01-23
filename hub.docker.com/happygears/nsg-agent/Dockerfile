
FROM maven:3-jdk-8-slim  as build

RUN  apt-get -y update && \
     apt-get install -y git rpm file findutils ruby ruby-dev libffi-dev gcc make cpio

RUN  gem install fpm

RUN  rm -rf /usr/src/app && mkdir -p /usr/src/app

COPY pom.xml        /usr/src/app
COPY agent-core     /usr/src/app/agent-core
COPY doc            /usr/src/app/doc
COPY getdown        /usr/src/app/getdown
COPY rpm            /usr/src/app/rpm
COPY tools          /usr/src/app/tools
COPY .git           /usr/src/app/.git

WORKDIR /usr/src/app

RUN pwd
RUN ls -la

# this builds both rpm and deb packages
RUN cd rpm && mvn package -B

#############################################################################
FROM openjdk:8-jre-stretch

ENV NSG_CURRENT="/opt/nsg-agent/current"
ENV NSG_HOME="/opt/nsg-agent/home"

RUN apt-get -y update && \
    apt-get install -y iputils-ping fping sed traceroute rsyslog rsyslog-relp less procps openjdk-8-jre-headless aptitude && \
    apt-get clean all

#RUN mkdir -p $NSG_HOME/        && \
#    mkdir -p $NSG_CURRENT/bin/ && \
#    mkdir -p $NSG_CURRENT/doc/ && \
#    mkdir -p $NSG_CURRENT/lib/

COPY --from=build /usr/src/app/rpm/target/rpm/nsg-agent*/RPMS/noarch/nsg-agent*.deb /root
RUN dpkg -i /root/nsg-agent*.deb

RUN ls -lRa /opt/nsg-agent/
RUN ls -la /etc/init.d/nsg-agent*

COPY docker/run.sh       /run.sh

# create this directory early to make sure it is chown'd to nw2
RUN mkdir -p ${NSG_HOME}/data/kafka/ssl

#RUN useradd --system -s /bin/bash -U -m --home-dir ${NSG_HOME} nw2
#RUN useradd -ms /bin/bash nw2
#RUN chmod +x $NSG_CURRENT/bin/*
#RUN chown -R nw2.nw2 $NSG_HOME && chown -R nw2.nw2 $NSG_CURRENT
RUN chown -R nw2.nw2 /var/spool/rsyslog

USER nw2

CMD exec /run.sh



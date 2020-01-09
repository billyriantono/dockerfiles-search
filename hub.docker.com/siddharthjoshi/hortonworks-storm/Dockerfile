FROM centos:7

## Install Oracle JDK 8


##RUN wget https://download.oracle.com/otn/java/jdk/8u221-b11/230deb18db3e4014bb8e3e8324f81b43/jdk-8u221-linux-x64.tar.gz

##RUN wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "https://download.oracle.com/otn/java/jdk/8u221-b11/230deb18db3e4014bb8e3e8324f81b43/jdk-8u221-linux-x64.tar.gz"

##wget --header "Cookie: oraclelicense=accept-securebackup-cookie" https://download.oracle.com/otn/java/jdk/8u221-b11/230deb18db3e4014bb8e3e8324f81b43/jdk-8u221-linux-x64.tar.gz

## Install Open JDK 7

##RUN yum install -y java-1.7.0-openjdk java-1.7.0-openjdk-devel

RUN yum install -y java-1.8.0-openjdk java-1.8.0-openjdk-devel

#RUN mkdir /usr/java && ln -s /usr/hdp/current/jvm/java-1.7.0-openjdk-1.7.0.51.x86_64 /usr/java/default 

#RUN export JAVA_HOME=/usr/java/default && export PATH=$JAVA_HOME/bin:$PATH && yum install -y wget


## Add Hortonworks Repo

##RUN wget -nv http://public-repo-1.hortonworks.com/HDP/centos7/2.x/updates/2.6.3.0/hdp.repo

##RUN yum-config-manager --add-repo http://public-repo-1.hortonworks.com/HDP/centos7/2.x/updates/2.6.3.0/hdp.repo

RUN yum-config-manager --add-repo http://public-repo-1.hortonworks.com/HDP/centos7/3.x/updates/3.1.0.0/hdp.repo

RUN yum install -y ntp && chkconfig ntpd on

##RUN setenforce 0

## Define environemnt variables
ENV STORM_CONF_DIR=/etc/storm/conf \
    STORM_DATA_DIR=/etc/storm/data \
    STORM_LOG_DIR=/etc/storm/logs 

## Create group and system user

RUN groupadd -r storm; \
    useradd -r -g storm storm
##adduser storm


## Install Storm

RUN yum install -y storm; \
    mkdir -p "$STORM_CONF_DIR" "$STORM_DATA_DIR" "$STORM_LOG_DIR"; \
    chown -R storm:storm "$STORM_CONF_DIR" "$STORM_DATA_DIR" "$STORM_LOG_DIR"; \
    chmod -R 755 /etc/storm; \
    rm "$STORM_CONF_DIR/storm.yaml"
#    && touch /etc/storm/conf/storm.yaml

#RUN mkdir -p /etc/storm/data /etc/storm/logs \
#    chown -R storm:storm "$STORM_CONF_DIR" "$STORM_DATA_DIR" "$STORM_LOG_DIR" \
#    chmod -R 755 /etc/storm

#RUN cat << EOF > "/etc/storm/conf/storm.yaml" \
#storm.zookeeper.servers: "zookeeper" \
#nimbus.seeds: "$STORM_NIMBUS_SEEDS" \
#storm.log.dir: "$STORM_LOG_DIR" \
#storm.local.dir: "$STORM_DATA_DIR" \
#EOF
#RUN chown -R storm:storm "$STORM_CONF_DIR" "$STORM_DATA_DIR" "$STORM_LOG_DIR" \
#    chmod -R 755 /etc/storm

#RUN echo 'storm.zookeeper.servers: "zookeeper"' \
#'nimbus.seeds: "nimbus"' \
#'storm.log.dir: "/etc/storm/logs"' \
#'storm.local.dir: "/etc/storm/data"' >> /etc/storm/conf/storm.yaml
#RUN yum -y install epel-release; \
#    yum -y update; 
#    yum -y install gosu

## To build locally
# COPY docker-entrypoint.sh /
## To build on Dockerhub
COPY /Storm/Docker/docker-entrypoint.sh /docker-entrypoint.sh
##COPY docker-entrypoint.sh /docker-entrypoint.sh
RUN ["chmod", "+x", "/docker-entrypoint.sh"]
ENTRYPOINT ["sh", "/docker-entrypoint.sh"]
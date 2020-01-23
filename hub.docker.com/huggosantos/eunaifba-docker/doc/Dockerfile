# Version 0.0.1

FROM centos:7

MAINTAINER HuBo <hubo@21cn.com>

ENV JDK_VERSION java-1.8.0-openjdk-devel
ENV MYSQL_RPM mysql57-community-release-el7-7.noarch.rpm

RUN curl http://repo.mysql.com/${MYSQL_RPM} -o ${MYSQL_RPM} \
	&& rpm -Uvh ${MYSQL_RPM} \
	&& rm ${MYSQL_RPM}

RUN yum update -y && yum -y install ${JDK_VERSION} mysql-community-server && yum clean all

RUN mysqld_pre_systemd


ENV WILDFLY_VERSION 10.0.0.Final
ENV WILDFLY_SHA1 c0dd7552c5207b0d116a9c25eb94d10b4f375549
ENV JBOSS_HOME /opt/jboss/wildfly

RUN curl -O https://download.jboss.org/wildfly/$WILDFLY_VERSION/wildfly-$WILDFLY_VERSION.tar.gz \
    && sha1sum wildfly-$WILDFLY_VERSION.tar.gz | grep $WILDFLY_SHA1 \
    && tar xf wildfly-$WILDFLY_VERSION.tar.gz \
    && mkdir -p /opt/jboss \
    && mv wildfly-$WILDFLY_VERSION $JBOSS_HOME \
    && rm wildfly-$WILDFLY_VERSION.tar.gz \
    && /opt/jboss/wildfly/bin/add-user.sh admin admin#1234 --silent

VOLUME /var/lib/mysql
VOLUME /opt/jboss/wildfly/standalone

EXPOSE 8080

ENTRYPOINT mysqld --user=mysql --skip-grant-tables & \
	exec /opt/jboss/wildfly/bin/standalone.sh -b 0.0.0.0 -bmanagement 0.0.0.0



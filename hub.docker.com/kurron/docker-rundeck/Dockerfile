# administrator account: admin/admin
# user account: user/user

FROM kurron/docker-oracle-jdk-8:latest

MAINTAINER Ron Kurr <kurr@kurron.org>

LABEL org.kurron.product.name="Rundeck" org.kurron.product.version=2.6.2

RUN mkdir -p /opt/rundeck

ADD http://dl.bintray.com/rundeck/rundeck-maven/rundeck-launcher-2.6.2.jar /opt/rundeck/rundeck.jar

EXPOSE 4440
EXPOSE 4443

VOLUME ["/opt/rundeck/server/data"]
VOLUME ["/opt/rundeck/server/config"]
VOLUME ["/opt/rundeck/etc"]
VOLUME ["/opt/rundeck/projects"]

#VOLUME ["/etc/rundeck", "/var/rundeck", "/var/lib/rundeck", "/var/lib/mysql", "/var/log/rundeck"]

ENV RDECK_BASE=/opt/rundeck

WORKDIR /opt/rundeck
ENTRYPOINT ["java", "-Drundeck.jetty.connector.forwarded=true", "-jar", "rundeck.jar"]

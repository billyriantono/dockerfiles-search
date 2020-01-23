FROM dockerfile/java:oracle-java8
MAINTAINER suk2 "yosuke.otsuka@develhack.com"

RUN dpkg-divert --local --rename --add /sbin/initctl
RUN echo "deb http://downloads.sourceforge.net/project/sonar-pkg/deb binary/" >> /etc/apt/sources.list
RUN apt-get update && apt-get upgrade -y

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y --force-yes  mysql-server sonar supervisor

# Configure MySql.
ADD create_database.sql /tmp/create_database.sql
ADD create_database.sh /tmp/create_database.sh
RUN sed -i -e 's|^bind-address\s*=\s*127.0.0.1|bind-address = 0.0.0.0|' /etc/mysql/my.cnf
RUN chmod +x /tmp/create_database.sh && /tmp/create_database.sh

# Configure SonarQube.
RUN sed -i -e 's|^#wrapper.java.additional.6=-server|wrapper.java.additional.6=-server|' /opt/sonar/conf/wrapper.conf
RUN sed -i -e 's|^sonar.jdbc.url=jdbc:h2|#sonar.jdbc.url=jdbc:h2|' /opt/sonar/conf/sonar.properties
RUN sed -i -e 's|^#sonar.jdbc.url=jdbc:mysql|sonar.jdbc.url=jdbc:mysql|' /opt/sonar/conf/sonar.properties
RUN sed -i -e 's|^#sonar.web.context=|sonar.web.context=${env:WEB_CONTEXT}|' /opt/sonar/conf/sonar.properties

# Configure Supervisor.
ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf
RUN mkdir -p /var/log/supervisor

# Configure volumes.
VOLUME ["/var/lib/mysql", "/var/log/mysql", "/var/log/supervisor"]

# Expose ports.
EXPOSE 3306 9000

# Start.
CMD ["/usr/bin/supervisord", "-n"]

FROM jeffbelback/centos-oracle-jre8

MAINTAINER Jeff Belback <mail@jeffbelback.me>

ENV TEAMCITY_DATA_PATH /data/teamcity

# Set JRE_HOME
ENV JRE_HOME /usr/java/default/

# Install utilities
RUN yum -y install tar wget

# Download and install TeamCity to /opt
ENV TEAMCITY_PKG TeamCity-8.1.5.tar.gz
ENV TEAMCITY_BASE_URL http://download.jetbrains.com/teamcity
RUN wget $TEAMCITY_BASE_URL/$TEAMCITY_PKG
RUN echo "6f3d709b130789dbc1e451be2202fff8952c8235c57e3379652e01841becf75c *TeamCity-8.1.5.tar.gz" >> TC_SHA256
RUN sha256sum $TEAMCITY
RUN tar zxf $TEAMCITY_PKG -C /opt && \
    rm -rf $TEAMCITY_PKG

# Download and install MYSQL JDBC Driver
ENV MYSQL_PKG mysql-connector-java-5.1.39.tar.gz
ENV MYSQL_BASE_URL http://dev.mysql.com/get/Downloads/Connector-J
RUN mkdir -p $TEAMCITY_DATA_PATH/lib/jdbc
RUN wget $MYSQL_BASE_URL/$MYSQL_PKG
RUN echo "c8988d4fc6e44364a2f51efe5b5139c1  "$MYSQL_PKG >> MD5SUM
RUN md5sum -c MD5SUM
RUN tar zxf mysql-connector-java-5.1.39.tar.gz -C /data/teamcity/lib
RUN cp /data/teamcity/lib/mysql*/mysql*.jar /data/teamcity/lib/jdbc/
RUN rm -rf /data/teamcity/lib/mysql*/ 
RUN rm -rf $MYSQL_PKG MD5SUM

EXPOSE 8111
CMD ["/opt/TeamCity/bin/teamcity-server.sh", "run"]

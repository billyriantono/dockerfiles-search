#inherit from yanhiro/docker-java image
FROM yanhiro/docker-java
MAINTAINER yanhiro <fjallot@fwfa-consulting.com>

#TEAMCITY DL VARIABLES
ENV TEAMCITY_DOWNLOAD_URL http://download-cf.jetbrains.com/teamcity
ENV TEAMCITY_PACKAGE TeamCity-9.1.1.tar.gz

#TEAMCITY INSTALL VARIABLES
ENV TEAMCITY_INSTALL_DIR /opt
ENV TEAMCITY_DATA_PATH /data/teamcity

#JDBC VARIABLES
ENV POSTGRES_JDBC_DOWNLOAD_URL https://jdbc.postgresql.org/download
ENV POSTGRES_JDBC_PACKAGE postgresql-9.4-1201.jdbc41.jar

#DB VARIABLES
ENV DB_HOSTNAME postgres
ENV DB_PORT 5432
ENV DB_DATABASE postgres
ENV DB_USERNAME postgres
ENV DB_PASSWORD=

#Postgres config file (template)
RUN mkdir -p /postgres/config
ADD database.postgresql.properties /postgres/config/database.properties

#JDBC driver
RUN mkdir -p /postgres/lib/jdbc
RUN wget $POSTGRES_JDBC_DOWNLOAD_URL/$POSTGRES_JDBC_PACKAGE
RUN mv $POSTGRES_JDBC_PACKAGE /postgres/lib/jdbc

#Copy config and run teamcity
ADD /scripts/run.sh /scripts/run.sh
RUN chmod +x /scripts/run.sh

# Download and install TeamCity to /opt
RUN wget -qO- $TEAMCITY_DOWNLOAD_URL/$TEAMCITY_PACKAGE | tar xz -C /opt

# Store TeamCity data in a volume to facilitate container upgrade
VOLUME  ["/data/teamcity"]

EXPOSE 8111
CMD /scripts/run.sh
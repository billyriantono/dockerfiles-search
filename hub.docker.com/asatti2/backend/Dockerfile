FROM sonodar/jdk8-tomcat8
MAINTAINER "Gaurav Sahu <gaurav.sahu13211@gmail.com>"

# Set frontend to be noninteractive to avoid any setup time prompts
ENV DEBIAN_FRONTEND noninteractive

# Add Tomcat Conf file to view Admin Console
ADD tomcat-users.xml /usr/local/tomcat/conf/

RUN apt-get update  
# Install cron
RUN apt-get install -y cron-apt
# Install maven
RUN apt-get install -y maven
# Install MySQL server
RUN apt-get install -y mysql-server

# Run cron related steps for MySQL dumps
# Add crontab file in the cron directory
ADD etc/cron.d/mysql /etc/cron.d/mysql

# Give read/write on the crontab file for root
RUN chmod 0644 /etc/cron.d/mysql
 
# Create the log file to be able
RUN touch /var/log/cron.log
 
# Activate crontab for root
RUN crontab /etc/cron.d/mysql
 
# Base folder which will contain source code
WORKDIR /code

# Adding MySQL dump script
ADD scripts/mysql_dump.sh /code/mysql_dump.sh

# Give execution rights on dump script for root
RUN chmod 700 /code/mysql_dump.sh

# Prepare by downloading dependencies
ADD pom.xml /code/pom.xml  

# Adding source, compile and package into a fat war
ADD src /code/src  
RUN ["mvn", "clean"]
RUN ["mvn", "install", "-P", "test"]

# Copy target war to Tomcat webapps dir
RUN cp target/oneapplication.war ${CATALINA_HOME}/webapps/oneapplication.war

# Add SQL DDL file
ADD oneapplication.sql /tmp/oneapplication.sql

# Create Database & Import dump file
RUN /bin/bash -c "/usr/bin/mysqld_safe &" && \
	sleep 5 && \
	mysql -u root -e "CREATE DATABASE 1application" && \
	mysql -u root -e "GRANT ALL ON 1application.* TO 'oa'@'localhost' IDENTIFIED BY 'root'" &&  \
	mysql -u root 1application < /tmp/oneapplication.sql

# Run SQL Service & Tomcat
CMD service cron start && service mysql start && /opt/tomcat/bin/catalina.sh run
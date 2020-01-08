FROM docker.io/ubuntu:18.10
MAINTAINER Viktor Horvath <support@reaction-engine.org>

# create folder for the reaction components
RUN mkdir /local && mkdir /local/reaction

# create the 'reaction' Linux user
RUN useradd -m -p $1$oqsJdAwa$m4W9ArsVZnXIXlru90y/e. reaction && echo reaction:reaction | chpasswd && gpasswd -a reaction sudo

# update the repositories and install vim, wget and unzip
RUN apt-get update -y && apt-get install -y vim wget unzip

# install sudo && change the pwd of root
RUN apt-get install -y sudo && echo root:root | chpasswd

#############################################################################
#                    1. install management app GUI
#############################################################################

# install mariadb
RUN apt-get install -y mariadb-server
# executing the content of 'mysql_secure_installation' script
RUN service mysql start && mysqladmin -u root password "root" \
    && mysql -u root -p"root" -e "UPDATE mysql.user SET Password=PASSWORD('root') WHERE User='root'" \
    && mysql -u root -p"root" -e "DELETE FROM mysql.user WHERE User='root' AND Host NOT IN ('localhost', '127.0.0.1', '::1')" \
    && mysql -u root -p"root" -e "DELETE FROM mysql.user WHERE User=''" \
    && mysql -u root -p"root" -e "DELETE FROM mysql.db WHERE Db='test' OR Db='test\_%'" \
    && mysql -u root -p"root" -e "FLUSH PRIVILEGES"
# allow remote access and using case-insensitive table names
RUN sed -i 's/bind-address/#bind-address/g' /etc/mysql/mariadb.conf.d/50-server.cnf && sed -i "s/myisam_recover_options  = BACKUP/myisam_recover_options  = BACKUP\nlower_case_table_names  = 1/g" /etc/mysql/mariadb.conf.d/50-server.cnf
# create reaction database
RUN mkdir /local/reaction/db
RUN service mysql start && mysql -u root -Bse  'create database reactionstore CHARACTER SET = "latin1";\
use reactionstore;\
CREATE USER "reaction"@"%" IDENTIFIED BY "reaction";\
GRANT ALL PRIVILEGES ON * . * TO "reaction"@"%";\
FLUSH PRIVILEGES;'

# install tools for python3
RUN apt-get install -y python3-venv python3-dev python3-pip
# creating a virtual environment 
RUN /usr/bin/python3.6 -m venv /local/reaction/environments/reaction-venv

# install Apache2 with mod_wsgi
RUN apt-get install -y apache2 apache2-dev
RUN apt-get install build-essential && /bin/bash -c "source /local/reaction/environments/reaction-venv/bin/activate && pip install -I mod_wsgi==4.6.4"

# download & unzip the management app install ZIP
RUN wget https://bitbucket.org/ric_flair_wcw/reaction-storage-v1_1/downloads/reaction_management_app_v1_1.zip -P /local/reaction/install/management_app
RUN unzip /local/reaction/install/management_app/reaction_management_app_v1_1.zip -d /local/reaction/install/management_app && rm -f /local/reaction/install/management_app/reaction_management_app_v1_1.zip

# install python's dependencies
RUN apt-get install -y libssl-dev libffi-dev && apt-get install -y language-pack-en
RUN /bin/bash -c "source /local/reaction/environments/reaction-venv/bin/activate && export LC_ALL=en_US.UTF-8 && export LC_CTYPE=en_US.UTF-8 && pip install wheel && pip install -r /local/reaction/install/management_app/requirements.txt"

# unzip the management app source ZIP
RUN unzip /local/reaction/install/management_app/management_app-1.1.zip -d /local/reaction/management_app

# configure settings_reaction.py: altering the database type from Oracle to mysql, the port number and the path of the log file
RUN sed -i "s|'filename' : 'reaction_debug.log'|'filename' : '/tmp/reaction_debug.log'|g" /local/reaction/management_app/management_app/settings_reaction.py
RUN sed -i "s|'ENGINE': 'django.db.backends.oracle'|'ENGINE': 'django.db.backends.mysql'|g" /local/reaction/management_app/management_app/settings_reaction.py
RUN sed -i "s|'PORT': '1521'|'PORT': '3306', 'OPTIONS': { 'autocommit': False, }|g" /local/reaction/management_app/management_app/settings_reaction.py

# initializing database schema of reaction by executing the 'makemigration' and 'migrate' Django command and execute the downloaded reaction_mysql.sql and the init_tables.sql (it contains sample data)
RUN sed -i '1s/^/import pymysql\npymysql.install_as_MySQLdb()\n/' /local/reaction/management_app/management_app/settings_reaction.py
RUN /bin/bash -c "source /local/reaction/environments/reaction-venv/bin/activate &&\
 service mysql start &&\
 cd /local/reaction/management_app &&\
 python manage.py makemigrations admin_system admin_execution_flow admin_errordetector monitoring scheduler common worker_status &&\
 python manage.py migrate"
COPY docker_demo_init_tables.sql /local/reaction/install/management_app
RUN service mysql start &&\
 mysql -h "localhost" -u "reaction" "-preaction" "reactionstore" < "/local/reaction/install/management_app/reaction_mysql.sql" &&\
 mysql -h "localhost" -u "reaction" "-preaction" "reactionstore" < "/local/reaction/install/management_app/docker_demo_init_tables.sql"

# configuring apache
RUN echo '<VirtualHost *:80>\n\
  ServerAdmin webmaster@localhost\n\
  ErrorLog ${APACHE_LOG_DIR}/error.log\n\
  CustomLog ${APACHE_LOG_DIR}/access.log combined\n\
  LoadModule wsgi_module /local/reaction/environments/reaction-venv/lib/python3.6/site-packages/mod_wsgi/server/mod_wsgi-py36.cpython-36m-x86_64-linux-gnu.so\n\
  Alias /reaction-management/static /local/reaction/management_app/static\n\
  <Directory /local/reaction/management_app/static>\n\
    Allow from all\n\
    Require all granted\n\
  </Directory>\n\
  <Directory /local/reaction/management_app/management_app>\n\
    <Files wsgi.py>\n\
      Require all granted\n\
    </Files>\n\
  </Directory>\n\
  WSGIDaemonProcess management-app python-path=/local/reaction/management_app/management_app:/local/reaction/environments/reaction-venv/lib/python3.6/site-packages\n\
  WSGIProcessGroup management-app\n\
  WSGIScriptAlias /reaction-management /local/reaction/management_app/management_app/wsgi.py process-group=management-app\n\
  PassEnv REACTION_SUBDOMAIN\n\
</VirtualHost>' > /etc/apache2/sites-available/000-default.conf
RUN echo "export REACTION_SUBDOMAIN=reaction-management" >> /etc/apache2/envvars
RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf && touch /tmp/reaction_debug.log && chmod a+wr /tmp/reaction_debug.log

#############################################################################
#                      2. install Reaction Engine
#############################################################################
# installing jdk
RUN apt-get -y install openjdk-8-jdk && echo "export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64" >> /home/reaction/.bashrc
# creating Linux user for Tomcat
RUN groupadd tomcat && useradd -s /bin/false -g tomcat -d /opt/tomcat tomcat
# getting the ZIP and unzip it
RUN wget https://archive.apache.org/dist/tomcat/tomcat-8/v8.5.27/bin/apache-tomcat-8.5.27.tar.gz -P /tmp/ && mkdir /opt/tomcat && tar xzvf /tmp/apache-tomcat-8*tar.gz -C /opt/tomcat --strip-components=1
# setting the permissions
RUN cd /opt/tomcat && chgrp -R tomcat /opt/tomcat && chmod -R g+r conf && chmod g+x conf && chown -R tomcat webapps/ work/ temp/ logs/

# downloading the WAR, config file, log config file
RUN mkdir /local/reaction/reaction-engine &&\
 wget https://bitbucket.org/ric_flair_wcw/reaction-storage-v1_1/downloads/reaction-engine-tomcat-1.1.war -P /local/reaction/install/reaction-engine &&\ 
 wget https://bitbucket.org/ric_flair_wcw/reaction-storage-v1_1/downloads/reaction-engine-config-1.1.zip -P /local/reaction/install/reaction-engine &&\
 unzip /local/reaction/install/reaction-engine/reaction-engine-config-1.1.zip -d /local/reaction/reaction-engine

# copying the WAR file to tomcat/webapps
RUN mv /local/reaction/install/reaction-engine/reaction-engine-tomcat-1.1.war /local/reaction/install/reaction-engine/reaction-engine.war &&\
 chmod a+w /local/reaction/install/reaction-engine/reaction-engine.war &&\
 cp /local/reaction/install/reaction-engine/reaction-engine.war /opt/tomcat/webapps
# setting the starting parameter of reaction engine to tomcat (altering /opt/tomcat/bin/setenv.sh)
RUN touch /opt/tomcat/bin/setenv.sh &&\
 echo 'CATALINA_OPTS="-Dspring.profiles.active=threadPool -Dspring.config.location=/local/reaction/reaction-engine/reaction-engine-application.yml -Dreaction.logback.config=/local/reaction/reaction-engine/logback-include.xml"' >> /opt/tomcat/bin/setenv.sh &&\
 chmod a+x /opt/tomcat/bin/setenv.sh
# setting the log file location
RUN sed -i "s|<file>reaction-engine.log</file>|<file>/tmp/reaction-engine.log</file>|g" /local/reaction/reaction-engine/logback-include.xml &&\
  sed -i "s|credentials_file: file:/local/reaction/engine/security/credentials|credentials_file: file:/local/reaction/reaction-engine/credentials|g" /local/reaction/reaction-engine/reaction-engine-application.yml
# setting the credentials of worker and management app web for authentication
RUN touch /local/reaction/reaction-engine/credentials &&\
 echo "ACME01=f0dedb78-3eb6-4a56-8428-e8e40584a01c" >> /local/reaction/reaction-engine/credentials &&\
 echo "reaction-management-web-app=e5574bf1-13c5-476a-b1d3-500bc640564d" >> /local/reaction/reaction-engine/credentials

#############################################################################
#                           3. install worker
#############################################################################
# downloading the worker
RUN wget https://bitbucket.org/ric_flair_wcw/reaction-storage-v1_1/downloads/reaction-worker-1.1-1.el7.noarch.rpm -P /local/reaction/install/worker

# intalling jsvc
RUN apt-get install -y jsvc
# installing the worker
RUN apt-get -y install alien
RUN alien -i /local/reaction/install/worker/reaction-worker-1.1-1.el7.noarch.rpm
RUN chmod a+x /local/reaction/worker-1.1/reaction_*.sh
# configuring the worker: setting the JAVA_HOME in manager_*.sh
RUN sed -i 's|J_HOME=$JAVA_HOME|J_HOME=/usr/lib/jvm/java-8-openjdk-amd64|g' /local/reaction/worker-1.1/reaction_reader.sh && sed -i 's|J_HOME=$JAVA_HOME|J_HOME=/usr/lib/jvm/java-8-openjdk-amd64|g' /local/reaction/worker-1.1/reaction_executor.sh

################### OTHERS #####################
# creating script to start the reaction services
################################################
RUN echo "echo reaction | sudo --stdin service mysql start && sudo service apache2 start && sudo /opt/tomcat/bin/startup.sh && echo Sleeping for 45 sec in order to give time Reaction Engine to start && sleep 45 && sudo /local/reaction/worker-1.1/reaction_reader.sh start && sudo /local/reaction/worker-1.1/reaction_executor.sh start" >> /local/reaction/start_reaction_services.sh && chmod a+rx /local/reaction/start_reaction_services.sh

RUN mv /usr/lib/python3.6/statistics.py /usr/lib/python3.6/_statistics.py_

EXPOSE 80 8080 3306

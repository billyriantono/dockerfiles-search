# CHOSING Debian
FROM debian:8.2

# APT-GET
RUN apt-get update
RUN apt-get upgrade
RUN apt-get install -y git
RUN apt-get install -y apache2
RUN apt-get install -y php5 php5-sqlite php5-mcrypt
RUN apt-get clean

# SET ENV
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid
ENV APACHE_RUN_DIR /var/run/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2

# ADDING DIRECTORIES
RUN mkdir -p $APACHE_RUN_DIR $APACHE_LOCK_DIR $APACHE_LOG_DIR

# CHANGING DIRECTORY
WORKDIR /var/www/html

# GET CSPHERE GIT 
RUN git clone https://github.com/csphere-cms/cSphere.git --branch dev --single-branch

# SETTING CSPHERE
RUN rm index.html
RUN cp -r cSphere/* .
RUN rm -r cSphere/ 
RUN chmod 777 csphere/config/
RUN chmod -R 777 csphere/storage/

# EXPOSE PORT FOR CSPHERE
EXPOSE 80

# START COMMAND
CMD ["/usr/sbin/apache2", "-D", "FOREGROUND"]
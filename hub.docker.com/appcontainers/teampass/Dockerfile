############################################################
# Dockerfile to build Teampass Container
# Based on: appcontainers/apache:centos
# DATE: 1/03/2016
# COPYRIGHT: Appcontainers.com
############################################################

# Set the base image to Centos 6.7 Apache Base
FROM appcontainers/apache:centos

# File Author / Maintainer
MAINTAINER Rich Nason rnason@appcontainers.com

###################################################################
#*************************  Reset Apache CTN  *********************
###################################################################

# This section will handle undoing any install magic that the apache base container did on setup.
RUN rm -fr /etc/httpd/conf.d/apache_cent.conf && \
rm -fr /var/www/*; mkdir -p /var/www/html && \
rm -fr /tmp/install.log && \
chown -R apache:apache /var/www/html && \
ls -lah /var/www

###################################################################
#*************************  APP VERSIONS  *************************
###################################################################

ENV TPVER TeamPass-2.1.25.2

###################################################################
#***************  OVERRIDE ENABLED ENV VARIABLES  *****************
###################################################################

ENV ENV dev
ENV TERMTAG teampass
ENV MODE standalone
ENV APP_NAME teampass.local
ENV APACHE_SVRALIAS www.teampass.local localhost
ENV MYSQL_SERVER localhost
ENV MYSQL_CLIENT localhost
ENV MYSQL_USER root
ENV MYSQL_PASS PAssw0rd
ENV MYSQL_DB teampass
ENV APP_USER admin
ENV APP_PASS PAssw0rd

###################################################################
#******************  ADD REQUIRED APP FILES  **********************
###################################################################

ADD apache_cent.conf /etc/httpd/conf.d/

###################################################################
#*******************  UPDATES & PRE-REQS  *************************
###################################################################

RUN yum clean all && \
yum -y update && \
yum -y install httpd mod_rewrite mod_ssl mod_env php php-common php-cli php-mysql php-xml php-pdo php-mcrypt \
php-mbstring php-bcmath php-openssl php-ldap mysql mysql-server perl unzip && \
yum clean all && \
rm -fr /var/cache/* && \

# Remove locales other than english
cd /usr/share/locale/ && \
for x in `ls | grep -v -i en | grep -v -i local`;do rm -fr $x; done && \
rm -fr ca* den men wen zen && \
cd /usr/lib/locale && \
localedef --list-archive | grep -v -i ^en | xargs localedef --delete-from-archive && \
mv -f locale-archive locale-archive.tmpl && \
build-locale-archive

###################################################################
#*******************  APPLICATION INSTALL  ************************
###################################################################

# Grab teampass and install it
ADD $TPVER.zip /var/www/html/
RUN cd /var/www/html/ && \
unzip $TPVER.zip && \
rm *.zip

# Set Max execution time in the PHP.ini file to 60 seconds
RUN sed -i 's/max_execution_time\ =\ 30/max_execution_time\ =\ 60/g' /etc/php.ini

###################################################################
#******************  POST DEPLOY CLEAN UP  ************************
###################################################################

###################################################################
#*****************  CONFIGURE START ITEMS  ************************
###################################################################

# Add Database Scripts, and Runconfig
ADD runconfig.sh /tmp/.runconfig.sh
ADD mysql_setup.sql /tmp/.mysql_setup.sql

RUN chmod +x /tmp/.runconfig.sh && \
echo "/tmp/./.runconfig.sh" >> ~/.bashrc && \
echo "[ -f /tmp/.runconfig.sh ] && rm -fr /tmp/.runconfig.sh" >> /root/.bashrc

# Set up Data Volume and Set docker run command.
CMD /bin/bash -c "/tmp/.runconfig.sh && service httpd stop && /usr/sbin/apachectl -D FOREGROUND"

###################################################################
#****************  EXPOSE APPLICATION PORTS  **********************
###################################################################

# Expose ports to other containers only
EXPOSE 80
EXPOSE 443
EXPOSE 3306

###################################################################
#*******************  OPTIONAL / LEGACY  **************************
###################################################################

############################################################
# Dockerfile to build a fully functional Laravel Container
# Based on appcontainers/centos66
############################################################

# Set the base image to Centos 6.6 Base
FROM appcontainers/centos66

# File Author / Maintainer
MAINTAINER Rich Nason rnason@appcontainers.com

#*************************
#*       Versions        *
#*************************
ENV FLYWAYVER flyway-3.2.1
ENV FWVER 3.2.1
ENV FWTARVER flyway-commandline-3.2.1.tar.gz
ENV MYSQLCONVER mysql-connector-java-5.1.35-bin.jar

#**********************************
#* Override Enabled ENV Variables *
#**********************************
ENV ENV prod
ENV TERMTAG LARAVEL
ENV APP_NAME laravel.local
ENV APACHE_SVRALIAS www.laravel.local localhost
ENV MYSQL_SERVER localhost
ENV MYSQL_CLIENT localhost
ENV MYSQL_USER root
ENV MYSQL_PASS PAssw0rd
ENV MYSQL_DB laravel
ENV APP_USER admin
ENV APP_PASS PAssw0rd
ENV MODE standalone
ENV SMB_ENABLE false
ENV SMB_USER samba
ENV SMB_PASS password


#*************************
#*  Update and Pre-Reqs  *
#*************************
RUN yum clean all && \
yum -y update && \
yum -y install httpd mod_rewrite mod_ssl mod_env php php-cli php-common php-mysql php-mysqlnd php-pgsql php-mcrypt php-json php-gd php-ldap php-pecl-jsonc php-xml php-process php-pear php-pdu php-mbstring mysql mysql-server unzip java-1.7.0-openjdk npm && \
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


#*************************
#*  Application Install  *
#*************************
# Install Bower
RUN npm install -g node && \
npm install -g bower

# Grab the composer.phar file
RUN cd /var/www/html/ && \
curl -sS https://getcomposer.org/installer | php

# Create the project
RUN php /var/www/html/composer.phar create-project laravel/laravel /var/www/html/$APP_NAME --prefer-dist

# Install bootstrap, jquery, Angular, lightbox, etc
RUN cd /var/www/html/$APP_NAME/ && \
echo "Ensure port 9418 outbound is open on your firewall !" && \
bower  init --allow-root --config.interactive && \
bower --allow-root --config.interactive=false install bootstrap --save && \
bower --allow-root --config.interactive=false install bootstrap-additions --save && \
bower --allow-root --config.interactive=false install angular --save && \
bower --allow-root --config.interactive=false install angular-route --save && \
bower --allow-root --config.interactive=false install angular-animate --save && \
bower --allow-root --config.interactive=false install angular-cookies --save && \
bower --allow-root --config.interactive=false install angular-loader --save && \
bower --allow-root --config.interactive=false install angular-resource --save && \
bower --allow-root --config.interactive=false install angular-sanitize --save && \
bower --allow-root --config.interactive=false install angular-touch --save && \
bower --allow-root --config.interactive=false install angular-strap --save && \
bower --allow-root --config.interactive=false install angular-motion --save && \
bower --allow-root --config.interactive=false install lightbox --save && \
bower --allow-root --config.interactive=false install datatables --save && \
bower --allow-root --config.interactive=false install jquery-ui --save && \
bower --allow-root --config.interactive=false install eonasdan-bootstrap-datetimepicker --save


#*************************
#*  Flyway Install  *
#*************************
# Download Flyway Database Migrations
RUN wget -P /tmp http://repo1.maven.org/maven2/org/flywaydb/flyway-commandline/$FWVER/$FWTARVER && \
tar -xzvf /tmp/$FWTARVER -C /var/www/html/$APP_NAME/database/ && \
rm -fr /tmp/$FWTARVER


#**************************
#*   Add Required Files   *
#**************************
ADD runconfig.sh /tmp/.runconfig.sh
ADD mysql_setup.sql /tmp/.mysql_setup.sql
ADD project.conf /etc/httpd/conf.d/
ADD $MYSQLCONVER /var/www/html/$APP_NAME/database/$FLYWAYVER/jars/
ADD flyway.conf /var/www/html/$APP_NAME/database/$FLYWAYVER/conf/
ADD smb.conf /tmp/


#************************
#* Post Deploy Clean Up *
#************************
# Change the project files permissions
RUN chown -R apache:apache /var/www/html/$APP_NAME && \
chmod -R 777 /var/www/html/$APP_NAME/storage


#**************************
#*  Config Startup Items  *
#**************************
RUN chmod +x /tmp/.runconfig.sh && \
echo "/tmp/./.runconfig.sh" >> /root/.bashrc && \
echo "rm -fr /tmp/.runconfig.sh" >> /root/.bashrc

CMD /bin/bash

#****************************
#* Expose Application Ports *
#****************************
# Expose ports to other containers only
EXPOSE 80
EXPOSE 138/udp
EXPOSE 139
EXPOSE 443
EXPOSE 445
EXPOSE 445/udp
EXPOSE 3306

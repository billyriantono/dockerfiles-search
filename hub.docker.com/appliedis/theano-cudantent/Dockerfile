############################################################
# Dockerfile to build a fully functional Laravel Container
# This container also incorporates full User Auth code
# Based on appcontainers/centos66
############################################################

# Set the base image to Centos 6.6 Base
FROM appcontainers/centos66

# File Author / Maintainer
MAINTAINER Rich Nason rnason@appcontainers.com

#*************************
#*       Versions        *
#*************************


#**********************************
#* Override Enabled ENV Variables *
#**********************************
ENV APP_NAME laravel.local
ENV APACHE_SVRALIAS www.laravel.local localhost
ENV MYSQL_SERVER localhost
ENV MYSQL_PASS P@ssw0rd
ENV MYSQL_DB laravel
ENV APP_USER admin
ENV APP_PASS P@ssw0rd
ENV SMB_USER samba
ENV SMB_PASS password


#**************************
#*   Add Required Files   *
#**************************
ADD runconfig.sh /tmp/
ADD mysql_setup.sql /tmp/
ADD project.conf /etc/httpd/conf.d/
ADD mysql-connector-java-5.1.31-bin.jar /tmp/
ADD flyway.properties /tmp/
ADD smb.conf /tmp/


#*************************
#*  Update and Pre-Reqs  *
#*************************
RUN yum clean all && \
yum -y update && \
yum -y install httpd mod_rewrite mod_ssl mod_env php php-cli php-common php-mysql php-pgsql php-mcrypt php-json php-gd php-ldap php-pecl-jsonc php-xml php-process php-pear php-pdu mysql mysql-server unzip tar java-1.7.0-openjdk git npm samba4 samba4-client && \
rm -fr /var/cache/*


#*************************
#*  Application Install  *
#*************************
# Install Bower
RUN npm install -g node && \
npm install -g bower

# Clone the AuthUserProject and remove the .git directory
RUN cd /var/www/html/ && git clone https://github.com/rnason/AuthUserShell.git && rm -fr AuthUserShell/.git

# Change the name of the project folder
RUN mv /var/www/html/AuthUserShell /var/www/html/$APP_NAME

# Install bootstrap, jquery, Angular, lightbox, etc
RUN cd /var/www/html/$APP_NAME/ && \
echo "Ensure port 9418 outbound is open" && \
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
RUN wget -P /tmp http://repo1.maven.org/maven2/org/flywaydb/flyway-commandline/3.0/flyway-commandline-3.0.tar.gz && \
tar -xzvf /tmp/flyway-commandline-3.0.tar.gz -C /var/www/html/$APP_NAME/app/database/ && \
mv /tmp/mysql-connector-java-5.1.31-bin.jar /var/www/html/$APP_NAME/app/database/flyway-3.0/jars/ && \
rm -fr /tmp/flyway-commandline-3.0.tar.gz

# Replace the Flyway Properties File
RUN cp -fr /tmp/flyway.properties /var/www/html/$APP_NAME/app/database/flyway-3.0/conf/


#************************
#* Post Deploy Clean Up *
#************************
# Change the project files permissions
RUN chown -R apache:apache /var/www/html/$APP_NAME && \
chmod -R 777 /var/www/html/$APP_NAME/app/storage


#************************
#* Add Samba            *
#************************
# Move the Samba Conf file
RUN mv /etc/samba/smb.conf /etc/samba/smb.conf.orig && \
mv /tmp/smb.conf /etc/samba/


#**************************
#*  Config Startup Items  *
#**************************
RUN chmod +x /tmp/runconfig.sh && \
echo "/tmp/./runconfig.sh" >> ~/.bashrc

CMD /bin/bash


#****************************
#* Expose Applicatoin Ports *
#****************************
# Expose ports to other containers only
EXPOSE 80
EXPOSE 138/udp
EXPOSE 139
EXPOSE 443
EXPOSE 445
EXPOSE 445/udp
EXPOSE 3306
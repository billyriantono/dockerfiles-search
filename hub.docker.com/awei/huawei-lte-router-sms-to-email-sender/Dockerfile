FROM ubuntu:14.04

MAINTAINER Maksym Nebot, <maksym.nebot@accenture.com>

#ENV VARIABLES
ENV LDAP_LTB_URL "ldap://ldap:389"
ENV LDAP_LTB_DN "cn=admin,dc=ldap,dc=example,dc=com"
ENV LDAP_LTB_PWD "changeme"
ENV LDAP_LTB_BS "dc=ldap,dc=example,dc=com"

# Install Apache2, PHP and LTB ssp
RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y apache2 php5 php5-mcrypt php5-ldap curl
RUN apt-get clean
RUN update-rc.d apache2 disable
RUN curl -LO http://ltb-project.org/archives/ltb-project-self-service-password-1.0.tar.gz
RUN mkdir -p /var/www/html/ltb
RUN tar zxf ltb-project-self-service-password-1.0.tar.gz -C /var/www/html/ltb --strip 1

# Configure self-service-password site
ADD assets/ltb.conf /etc/apache2/sites-available/ltb.conf
RUN php5enmod mcrypt
RUN php5enmod ldap
RUN a2dissite 000-default
RUN a2ensite ltb

# This is where configuration goes
ADD assets/config.inc.php /var/www/html/ltb/conf/config.inc.php

RUN mkdir -p /etc/service/apache2
ADD assets/apache2.sh /etc/service/apache2/run
CMD ["/etc/service/apache2/run"]

EXPOSE 80

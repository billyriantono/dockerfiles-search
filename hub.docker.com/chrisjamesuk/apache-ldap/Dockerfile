FROM centos/httpd:latest
MAINTAINER chris.james@1and1.co.uk
RUN \
  yum install mod_ldap -y &&\
  chmod 777 /run -R &&\
  chmod 777 /var/log -R 
EXPOSE 80
#ADD ldap.conf /etc/httpd/conf.d/ldap.conf

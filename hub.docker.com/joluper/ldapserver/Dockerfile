# Version: 0.0.1
FROM fedora
MAINTAINER @edt "ASIX M06/M11 @edt 2015-16"

# software
RUN yum -y install vim mlocate man-db procps iproute openldap openldap-servers openldap-clients 

# directoris
RUN mkdir /opt/docker

# fitxers
COPY * /opt/docker/
RUN chmod +x /opt/docker/install.sh /opt/docker/startup.sh
WORKDIR /opt/docker
COPY ldap.conf /etc/openldap/
RUN /opt/docker/install.sh
CMD ["/opt/docker/startup.sh"]


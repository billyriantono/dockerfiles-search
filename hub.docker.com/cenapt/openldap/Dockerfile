# Inspired from http://www.server-world.info/en/note?os=CentOS_7&p=openldap&f=1
FROM centos:7

ENV SLAPD_ROOT_PW test
ENV SLAPD_MANAGER_PW test
ENV SAMBA_PW test
ENV SLAPD_DC dc=auth,dc=example,dc=com
ENV SLAPD_NAME "Example LDAP"
ENV SLAPD_SERVERNAME auth

RUN yum -y update && yum -y clean all && yum -y install ca-certificates openldap openldap-servers openldap-clients sssd perl-LDAP.noarch samba gettext &&  yum -y clean all
RUN rm -rf /var/cache/yum
RUN mkdir /etc/openldap/local
COPY config/DB_CONFIG /etc/openldap/local
COPY config/slapd.ldif.tmpl /etc/openldap/local
COPY config/frontend.ldif.tmpl /etc/openldap/local
RUN chown -R ldap:ldap /etc/openldap/local
COPY scripts/setup.sh /
COPY scripts/run.sh /

EXPOSE 389 636
VOLUME ["/var/lib/ldap", "/etc/openldap/slapd.d", "/ssl"]
CMD /run.sh

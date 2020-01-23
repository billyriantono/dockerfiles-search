FROM openshift/openldap-2441-centos7
#Added a line
LABEL Description="This is a customization of an OpenLDAP install running that has been tested to run on RHEL 7.4. It is intended to carry a small subset of attributes that originate from IBM Bluepages. It is intended for IBM internal use only" Version="1.0"

ADD etc_openldap.tgz /etc/openldap
ADD var_lib_ldap.tgz /var/lib/ldap
CMD chown -R ldap.ldap /etc/openldap/slapd.d
CMD chown -R ldap.ldap /var/lib/ldap/*
ENTRYPOINT /usr/local/bin/run-openldap.sh

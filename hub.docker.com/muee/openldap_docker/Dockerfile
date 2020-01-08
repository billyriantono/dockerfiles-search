FROM osixia/openldap
LABEL Maintainer=matthias@oehm.at

ENV LDAP_ADMIN_PASSWORD blub
ENV LDAP_BACKEND mdb

RUN mkdir -p /install/openldap

ADD files/* /install/openldap/

# Datenbanktyp wegschreiben in die Dateien:
RUN chmod +x /install/openldap/add_memberof.sh
	
#CMD ["/bin/bash", "/install/openldap/add_memberof.sh"]
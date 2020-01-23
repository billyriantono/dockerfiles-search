FROM centos:6
MAINTAINER lx,lx.simon@yahoo.com

ENV CURDIR /opt/scripts
RUN yum update -y && yum install -y vim openssh openssh-clients openssh-server openldap openldap-clients openldap-servers openldap-servers-sql
RUN sed -i 's/com/cn/g' '/etc/openldap/slapd.d/cn=config/olcDatabase={2}bdb.ldif'
RUN sed -i 's/my-domain/baitu/g' '/etc/openldap/slapd.d/cn=config/olcDatabase={2}bdb.ldif'
RUN sed -i 's/com/cn/g' '/etc/openldap/slapd.d/cn=config/olcDatabase={1}monitor.ldif'
RUN sed -i 's/my-domain/baitu/g' '/etc/openldap/slapd.d/cn=config/olcDatabase={1}monitor.ldif'
RUN echo "olcRootPW: `slappasswd -h {MD5} -s "baituldap"`" >> '/etc/openldap/slapd.d/cn=config/olcDatabase={2}bdb.ldif'
RUN echo 'olcAccess: {0}to attrs=userPassword by self write by dn.base="cn=Manager,dc=baitu,dc=cn" write by anonymous auth by * none' >> '/etc/openldap/slapd.d/cn=config/olcDatabase={2}bdb.ldif'
RUN echo 'olcAccess: {1}to * by dn.base="cn=Manager,dc=baitu,dc=cn" write by self write by * read' >> '/etc/openldap/slapd.d/cn=config/olcDatabase={2}bdb.ldif'
ADD scripts ${CURDIR}
WORKDIR ${CURDIR}
EXPOSE 389
VOLUME [ "/var/lib/ldap" ]
ENTRYPOINT ["./ldap-entrypoint.sh"]
CMD [ "slapd", "-d", "256" ]


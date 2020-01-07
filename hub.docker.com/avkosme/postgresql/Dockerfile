FROM avkosme/centos

RUN yum -y install https://download.postgresql.org/pub/repos/yum/10/redhat/rhel-7-x86_64/pgdg-centos10-10-2.noarch.rpm
RUN yum -y install postgresql10
RUN yum -y install postgresql10-server

RUN systemctl enable postgresql-10

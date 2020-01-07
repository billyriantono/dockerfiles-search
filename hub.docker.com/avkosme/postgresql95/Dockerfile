FROM avkosme/centos

RUN yum -y install https://download.postgresql.org/pub/repos/yum/9.5/redhat/rhel-7-x86_64/pgdg-centos95-9.5-3.noarch.rpm
RUN yum -y install yum install postgresql95
RUN yum -y install postgresql95-server

RUN systemctl enable postgresql-9.5

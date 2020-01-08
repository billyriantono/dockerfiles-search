FROM centos:latest

RUN yum update -y
RUN yum install epel-release -y
RUN yum install python34 -y
RUN rpm -ivh http://repo.postgrespro.ru/pgpro-9.5/keys/postgrespro-9.5.centos95.noarch.rpm
RUN yum install postgrespro95-server postgrespro95-contrib  postgrespro95-plpython -y
RUN /etc/init.d/postgresql-9.5 initdb


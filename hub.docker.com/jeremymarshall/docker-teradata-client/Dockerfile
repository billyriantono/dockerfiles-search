FROM centos:centos7
  MAINTAINER Jeremy Marshall
  RUN yum -y install ksh && yum clean all

  ONBUILD ADD  tdodbc__linux_indep.*.tar.gz tmp/
  ONBUILD RUN pushd tmp && find . -name '*.tar.gz' -exec tar zxvf {} --strip=1 \; && popd
  ONBUILD RUN rpm -ivh --nodeps tmp/TeraGSS_linux_x64-15.*.noarch.rpm  tmp/tdicu-15.*.noarch.rpm  tmp/tdodbc-15.*.noarch.rpm; yum clean all;

  ENV ODBCHOME=/opt/teradata/client/ODBC_64/ ODBCINI=/opt/teradata/client/ODBC_64/odbc.ini


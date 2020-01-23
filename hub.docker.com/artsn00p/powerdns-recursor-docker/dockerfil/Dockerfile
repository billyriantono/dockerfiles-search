# Docker base image for general util
FROM centos:centos6
MAINTAINER Art

# Update yum
RUN yum makecache

RUN yum install -y zip
RUN yum install -y wget
RUN yum install -y epel-release

# Install FreeTDS
RUN yum -y install freetds freetds-devel

# Install SQSH
RUN wget http://sourceforge.net/projects/sqsh/files/sqsh/sqsh-2.5/sqsh-2.5-1.el6.x86_64.x86_64.rpm
RUN yum -y install sqsh-2.5-1.el6.x86_64.x86_64.rpm

# Install Python
RUN yum -y install python-pip
RUN yum -y install python-devel

RUN yum -y install gcc

# Install Python modules
RUN pip install pymssql
RUN pip install prettytable
RUN pip install argparse
RUN pip install unicodecsv
RUN pip install python-dateutil
RUN pip install gdata
RUN pip install google-api-python-client

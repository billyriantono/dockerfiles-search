FROM centos:centos6
MAINTAINER creisor@gmail.com

# reviewboard dependencies
RUN yum -y install httpd httpd-devel mod_wsgi gcc openssl-devel patch mysql-devel git-core wget

# install python 2.7 software collection
RUN yum -y install scl-utils scl-utils-build centos-release-SCL
RUN yum -y install python27
RUN yum -y install python27-mod_wsgi
RUN scl enable python27 'easy_install -U setuptools'
RUN scl enable python27 'easy_install mysql-python'

# install ReviewBoard
RUN scl enable python27 'easy_install ReviewBoard==2.0.11'

# remove devel stuff
RUN yum -y remove httpd-devel openssl-devel mysql-devel

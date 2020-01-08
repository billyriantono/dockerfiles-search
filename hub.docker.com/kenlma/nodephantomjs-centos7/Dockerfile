# !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
# NOTE: DO *NOT* EDIT THIS FILE.  IT IS GENERATED.
# PLEASE UPDATE Dockerfile.txt INSTEAD OF THIS FILE
# !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
FROM centos:7.2.1511

MAINTAINER Ken.l.ma

# phantomjs to 2.0.0

USER root

#==============
# PhantomJS
#==============
RUN yum update -y
RUN rpm --rebuilddb; yum install -y yum-plugin-ovl
RUN yum -y install gcc gcc-c++ make flex bison gperf ruby \
	openssl-devel freetype-devel fontconfig fontconfig-devel libicu-devel sqlite-devel \
	libpng-devel libjpeg-devel
COPY phantomjs /usr/local/bin/phantomjs
RUN chmod +x /usr/local/bin/phantomjs

#==============================
# Scripts to run Selenium Node
#==============================
COPY entry_point.sh \
	functions.sh \
    /opt/bin/
RUN chmod +x /opt/bin/entry_point.sh

#============================
# Some configuration options
#============================
#ENV SCREEN_WIDTH 1360
#ENV SCREEN_HEIGHT 1020
#ENV SCREEN_DEPTH 24
#ENV DISPLAY :99.0
#ENV NODE_APPLICATION_NAME ""


CMD ["/opt/bin/entry_point.sh"]

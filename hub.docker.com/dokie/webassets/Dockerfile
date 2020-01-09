# Webassetsr
#
# VERSION 0.0.1

# Building from CentOS 7
FROM centos:centos7
MAINTAINER i2O Water <anapos@i2owater.com>

# Add files.
COPY rpm/ /tmp

# Install Node.js v0.8.23
RUN yum -y update; yum clean all
RUN yum -y install /tmp/epel-release-6-8.noarch.rpm
RUN yum -y install /tmp/nodejs-0.8.23-1.x86_64.rpm
RUN yum -y install /tmp/protobuf-2.4.1-1.el6.i2o.x86_64.rpm
RUN npm install -g forever@0.11.1

#RUN yum -y install http://yum.uk01.i2owater.com/repo/i2o/RPMS/x86_64/nodejs-0.8.23-1.x86_64.rpm
#RUN yum -y install http://yum.uk01.i2owater.com/repo/i2o/RPMS/x86_64/protobuf-2.4.1-1.el6.i2o.x86_64.rpm

# Define environment variables.
ENV PATH /opt/node/bin:$PATH

# Define mount points.
VOLUME ["/data/var/lib/anapos"]

# Define working directory.
WORKDIR /data/var/lib/anapos

# Define default command.
CMD ["/data/var/lib/anapos/run_anapos.sh"]

# Expose ports.
EXPOSE 8001

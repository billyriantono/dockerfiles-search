FROM centos:7

# Import keys and fix passwd issue.
RUN rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

###########################################################
#***************  UPDATES & PRE-REQS  ********************#
###########################################################
# Clean, Update, and Install... then clear non English local data.
# NOTE: If building on any box other than a CentOS 7 docker host, then iputils.x86 will fail with:
# unpacking of archive failed on file /usr/bin/ping: cpio: cap_set_file
RUN yum clean all

# Install required packages
RUN yum -y install epel-release && \
     rpm --import http://download.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL-7

# Download and install Epel, and Remi repositories.
RUN curl -O http://rpms.remirepo.net/enterprise/remi-release-7.rpm \
&& rpm -Uvh remi-release-7.rpm \
&&  rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-remi \
&&  rm -fr *.rpm

#Enable the remi repo
RUN sed -ie '/\[remi\]/,/^\[/s/enabled=0/enabled=1/' /etc/yum.repos.d/remi.repo && \
    sed -ie '/\[remi-php55\]/,/^\[/s/enabled=0/enabled=1/' /etc/yum.repos.d/remi.repo && \
    sed -ie '/\[remi-php71\]/,/^\[/s/enabled=0/enabled=1/' /etc/yum.repos.d/remi-php71.repo

# Update the OS,
# Exclude systemd, and its dependant libs as centos installs a fake systemd for the container.
RUN yum -y update && yum clean all \
  &&  yum install -y \
              util-linux* \
              --exclude=systemd* \
              util-linux* \
              libblkid* \
              libuuid* \
              libmount* \
              net-tools \
              nano \
              wget \
              vim \
              ncdu \
              sudo

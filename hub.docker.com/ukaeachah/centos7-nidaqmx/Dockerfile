FROM centos:7

# Fetch and install the meta-rpm which adds NI's repository
RUN curl -sS -o ni-software.rpm http://download.ni.com/support/softlib//MasterRepository/ni-software-2018-18.0.1.49153-0+f1.el7.noarch.rpm

RUN rpm -iv ni-software.rpm

# Install NI daqmx software
# N.B. Pulls in a bunch of ni packages plus gcc, kernel-devel, avahi,
# Uncle Tom Cobbley and all (186 dependent packages)
RUN yum -y install ni-daqmx

# Other packages useful for building applications
RUN yum -y install make

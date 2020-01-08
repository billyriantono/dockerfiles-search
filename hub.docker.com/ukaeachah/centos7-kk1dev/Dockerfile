FROM ukaeachah/centos7-nidaqmx

# Other packages useful for building applications
RUN yum -y install make autoconf automake libtool

# For compilation of kk1rt
RUN yum -y install fftw-devel libcap-devel systemd-devel

# For releasing python modules
RUN yum -y install python-setuptools

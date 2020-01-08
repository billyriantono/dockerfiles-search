FROM centos:latest
MAINTAINER  Xin Zhang <xin.zhang@longrunweather.edu>
# 
# This Dockerfile compiles WRF from source during "docker build" step
ENV WRF_VERSION 3.9.1.1
ENV UPP_VERSION 3.2

#SERIAL BUILD
RUN yum -y update
RUN yum -y install file gcc gcc-gfortran gcc-c++ glibc.i686 libgcc.i686 libpng-devel jasper jasper-devel ksh hostname m4 make perl tar tcsh time wget which zlib zlib-devel epel-release
#
# now get 3rd party EPEL builds of netcdf dependencies
RUN yum -y install netcdf-devel.x86_64 netcdf-fortran-devel.x86_64 netcdf-fortran.x86_64 hdf5.x86_64
#
WORKDIR /wrf_serial
#
# Download original sources
#
RUN curl -SL http://www2.mmm.ucar.edu/wrf/src/WRFV${WRF_VERSION}.TAR.gz | tar zxC /wrf_serial \
 && curl -SL http://www.dtcenter.org/upp/users/downloads/UPP_releases/DTC_upp_v${UPP_VERSION}.tar.gz | tar zxC /wrf_serial
#

# Set environment for interactive container shells
#
RUN echo export LDFLAGS="-lm" >> /etc/bashrc \ 
 && echo export NETCDF=/wrf_serial/netcdf_links >> /etc/bashrc \
 && echo export JASPERINC=/usr/include/jasper/ >> /etc/bashrc \
 && echo export JASPERLIB=/usr/lib64/ >> /etc/bashrc \
 && echo export LD_LIBRARY_PATH="/usr/lib64" >> /etc/bashrc \
 && echo export PATH="/usr/lib64/bin:$PATH" >> /etc/bashrc \
 && echo setenv LDFLAGS "-lm" >> /etc/csh.cshrc \
 && echo setenv NETCDF "/wrf_serial/netcdf_links" >> /etc/csh.cshrc \
 && echo setenv JASPERINC "/usr/include/jasper/" >> /etc/csh.cshrc \
 && echo setenv JASPERLIB "/usr/lib64/" >> /etc/csh.cshrc \
 && echo setenv LD_LIBRARY_PATH "/usr/lib64" >> /etc/csh.cshrc \
 && echo setenv PATH "/usr/lib64/bin:$PATH" >> /etc/csh.cshrc
#
# Build WRF first
# input 34 and 1 to configure script alternative line = && echo -e "32\r1\r" | ./configure
# 
RUN pwd \ 
 && mkdir netcdf_links \
 && ln -sf /usr/include/ netcdf_links/include \
 && ln -sf /usr/lib64 netcdf_links/lib \
 && ln -sf /usr/lib64/gfortran/modules/netcdf.mod netcdf_links/include \
 && export NETCDF=/wrf_serial/netcdf_links \
 && export JASPERINC=/usr/include/jasper/ \
 && export JASPERLIB=/usr/lib64/ \
 && cd ./WRFV3 \
 && ./configure <<< $'32\r1\r' \
 && /bin/csh ./compile em_real > compile_wrf_arw_opt32.1.log 2>&1
#
# Build UPP second
#
# input 7 to configure script (for gfortran serial build)
RUN cd ./UPPV3.2 \
 && export NETCDF=/wrf_serial/netcdf_links \
 && ./configure <<< $'7\r' \
 && /bin/csh ./compile > compile_upp.log 2>&1
#
ENV LD_LIBRARY_PATH /usr/lib64/lib
ENV PATH  /usr/lib64/bin:$PATH
#


CMD ["/bin/bash" , "-l"]

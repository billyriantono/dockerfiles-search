FROM centos:7

RUN yum install -y gcc-gfortran curl fontconfig libXrender libXext libidn ImageMagick

RUN curl -SL https://www.earthsystemgrid.org/dataset/ncl.630.0/file/ncl_ncarg-6.3.0.Linux_CentOS7.0_x86_64_gcc482.tar.gz | tar -xzvC /usr
ENV NCARG_ROOT /usr

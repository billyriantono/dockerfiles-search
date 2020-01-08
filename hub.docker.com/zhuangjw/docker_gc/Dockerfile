FROM ubuntu:16.04
MAINTAINER Jiawei Zhuang <jiaweizhuang@g.harvard.edu>

RUN apt-get update && \
    apt-get install -y git vim bc gcc gfortran libnetcdf-dev libnetcdff-dev netcdf-bin

ENV CC=gcc CXX=g++ FC=gfortran
ENV F90=$FC F9X=$FC F77=$FC
ENV NETCDF_HOME=/usr NETCDF_FORTRAN_HOME=/usr
ENV GC_BIN=$NETCDF_HOME/bin \
    GC_INCLUDE=$NETCDF_HOME/include \
    GC_LIB=$NETCDF_HOME/lib \
    GC_F_BIN=$NETCDF_FORTRAN_HOME/bin \
    GC_F_INCLUDE=$NETCDF_FORTRAN_HOME/include \
    GC_F_LIB=$NETCDF_FORTRAN_HOME/lib

# fix Perl error message
ENV LANG C

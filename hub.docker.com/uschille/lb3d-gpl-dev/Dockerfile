FROM ubuntu:14.04
MAINTAINER Lev Shamardin <shamardin@gmail.com>
RUN apt-get update && apt-get install -y libhdf5-mpich2-dev gfortran git automake python-dev make hdf5-tools python-tables
# this is a workaround for Ubuntu HDF5 packaging bug
RUN ln -s /usr/bin/h5cc /usr/bin/h5pcc && ln -s /usr/bin/h5fc /usr/bin/h5pfc

RUN useradd -m lb3d

#RUN git clone --depth 1 https://78abdff51ac3e702b44f6dbc84f073dd6e47fe98:x-oauth-basic@github.com/UCL/lb3d-gpl-dev.git /home/lb3d/lb3d-gpl -b docker

COPY . /home/lb3d/lb3d-gpl
RUN chown -R lb3d:lb3d /home/lb3d/lb3d-gpl
 
USER lb3d
WORKDIR /home/lb3d/lb3d-gpl

RUN ./bootstrap
RUN ./configure --with-lb3d-py-path=$(pwd)/py
RUN make V=1 -j1 --debug=b
RUN make check

# Base development setup

FROM centos:latest
MAINTAINER imofftoseethewizard@github.com <Pat Lasswell>

RUN yum -y install autoconf automake bzip2 gcc gcc-c++ gcc-gfortran git m4 make patch perl tar wget

RUN mkdir -p /src/
WORKDIR /src/
RUN wget http://www.cmake.org/files/v3.0/cmake-3.0.0.tar.gz
RUN tar -zxvf cmake-3.0.0.tar.gz
WORKDIR cmake-3.0.0
RUN ./bootstrap
RUN gmake
RUN gmake install

RUN git clone git://github.com/JuliaLang/julia.git /src/julia
WORKDIR /src/julia/
RUN git checkout release-0.3
RUN make

CMD ["/bin/bash"]


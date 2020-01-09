FROM centos:8 as builder
WORKDIR /opt/src
RUN yum -y install cmake openssl-devel rpm-build
RUN yum -y install make
RUN yum -y install gcc-c++
RUN yum -y install cmake3
COPY . .
RUN mkdir -p build
WORKDIR /opt/src/build
RUN cmake3 .. -DCMAKE_BUILD_TYPE=Release && make -j4 && cpack3 -G RPM

FROM centos:6

ARG CMAKE_VERSION=3.14.2

RUN yum update -y \
    && yum install --setopt=tsflags=nodocs -y centos-release-scl \
    && yum install --setopt=tsflags=nodocs -y \
         gcc gcc-c++ devtoolset-8-binutils devtoolset-8-gcc devtoolset-8-gcc-c++ rpm-build \
         mysql-devel libcurl-devel \
    && yum clean all -y \
    && curl -SL https://cmake.org/files/LatestRelease/cmake-${CMAKE_VERSION}-Linux-x86_64.tar.gz | tar xz -C /usr/local/ --strip-component 1 

RUN yum update -y \
    && yum install --setopt=tsflags=nodocs -y flex byacc bison \
    && yum clean all -y
    
#COPY gsoap_2.8.22.zip /gsoap/
#RUN cd /gsoap/ && unzip gsoap_2.8.22.zip \
#    && cd /gsoap/gsoap-2.8/ && ./configure && make && make install \
#    && rm -fr /gsoap/

RUN mkdir /gsoap && cd /gsoap \
    && curl -SL https://sourceforge.net/projects/gsoap2/files/oldreleases/gsoap_2.8.22.zip -o gsoap.zip \
    && unzip gsoap.zip \
    && cd /gsoap/gsoap-2.8/ && ./configure && make && make install \
    && rm -fr /gsoap/

CMD ["/bin/bash"] 


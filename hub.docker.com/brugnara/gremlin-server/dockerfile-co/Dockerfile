FROM golang:1.13

ARG MPICH_VERSION="3.3.2"
 
RUN mkdir -p /tmp/mpich-src && \
      cd /tmp/mpich-src && \
      wget http://www.mpich.org/static/downloads/${MPICH_VERSION}/mpich-${MPICH_VERSION}.tar.gz && \ 
      tar xfz mpich-${MPICH_VERSION}.tar.gz && \ 
      cd mpich-${MPICH_VERSION} && \ 
      ./configure --disable-fortran -prefix=/mpich && \
      make && \
      make install && \
      cd /tmp && rm -rf mpich-src
ENV CGO_LDFLAGS='-L/mpich/lib/ -lmpich'
ENV PATH=/mpich/bin:$PATH
ENV CPLUS_INCLUDE_PATH=/mpich/include:/mpich/lib
ENV C_INCLUDE_PATH=/mpich/include:/mpich/lib
ENV LD_LIBRARY_PATH=/mpich/include:/mpich/lib

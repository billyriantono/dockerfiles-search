FROM gcc:4.9.2

RUN cd /opt \
  && curl https://cmake.org/files/v3.4/cmake-3.4.3-Linux-x86_64.tar.gz | tar zxf -

ENV LD_LIBRARY_PATH "$LD_LIBRARY_PATH:/usr/local/lib64:/usr/lib64"
ENV PATH "$PATH:/opt/cmake-3.4.3-Linux-x86_64/bin"


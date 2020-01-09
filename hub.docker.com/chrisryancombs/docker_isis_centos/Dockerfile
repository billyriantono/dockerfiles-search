FROM  centos:7

RUN yum install -y gcc-c++
RUN yum install -y wget bzip2 ca-certificates
RUN yum install -y which

RUN yum install -y xorg-x11-apps
RUN yum install -y mesa-libGL
RUN yum install -y mesa-libGLU-devel

RUN echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh && \
    wget --quiet https://repo.continuum.io/miniconda/Miniconda3-4.5.4-Linux-x86_64.sh -O ~/miniconda.sh && \
    /bin/bash ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh 
ENV PATH /opt/conda/bin:$PATH

RUN mkdir -p /workspace/ISIS3_cmake /workspace/ISIS3_cmake@tmp ./build ./install

ENTRYPOINT [ "/bin/bash", "-c", "--" ]

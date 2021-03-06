FROM ubuntu:18.10

# Install a few packages, as root
RUN apt-get update \
    && apt-get install -y \
    sudo \
    wget \
    autoconf \
    automake \
    make \
    git \
    vim \
    gcc \
    g++ \
    gfortran \
    zlib1g-dev \
    libffi-dev \
    libx11-dev \
    libssl-dev \
    && apt-get clean all \
    && rm -rf /var/lib/apt/lists/*

# Instructions from NERSC for manually building MPICH (updated)
# Note that using pip requires zlib1g-dev and libffi-dev.
RUN mkdir /build/

RUN cd /build && wget --no-check-certificate https://www.python.org/ftp/python/3.7.2/Python-3.7.2.tgz \
  && tar xvzf Python-3.7.2.tgz && cd /build/Python-3.7.2 \
  && ./configure --with-ensurepip=install && make -j4 && make install && make clean && rm /build/Python-3.7.2.tgz

RUN cd /build && wget --no-check-certificate https://www.mpich.org/static/downloads/3.3/mpich-3.3.tar.gz \
  && tar xvzf mpich-3.3.tar.gz && cd /build/mpich-3.3 \
  && ./configure && make -j4 && make install && make clean && rm /build/mpich-3.3.tar.gz

RUN cd /build && wget --no-check-certificate https://bitbucket.org/mpi4py/mpi4py/downloads/mpi4py-3.0.1.tar.gz \
  && tar xvzf mpi4py-3.0.1.tar.gz

RUN cd /build/mpi4py-3.0.1 && python3 setup.py build && python3 setup.py install && rm -rf /build/

RUN /sbin/ldconfig

# openPMD-viewer is installed mainly for tests
# Note: matplotlib is installed with pip3 since the apt-get install matplotlib
#       needs the time zone to be set.

RUN pip3 --no-cache-dir install \
    numpy \
    scipy \
    h5py \
    matplotlib \
    openPMD-viewer \
    Forthon

# Install pygist
ENV GIT_SSL_NO_VERIFY 1
RUN git clone https://bitbucket.org/dpgrote/pygist.git \
    && cd pygist \
    && python3 setup.py config \
    && python3 setup.py install \
    && cd ../ \
    && rm -rf pygist

# Create a new user and copy the current branch of Warp
# into the Docker container
RUN useradd --create-home warp_user
RUN mkdir /home/warp_user/warp/
COPY ./ /home/warp_user/warp/

# Compile warp
RUN cd /home/warp_user/warp/pywarp90 \
    && rm -f *local* \
    && echo 'FCOMP= -F gfortran' >> Makefile.local3 \
    && echo 'FCOMP= -F gfortran' >> Makefile.local3.pympi \
    && echo 'FCOMPEXEC= --fcompexec mpifort' >> Makefile.local3.pympi \
    && make install3 \
    && make clean3 \
    && make pinstall3 \
    && make pclean3

RUN chown -R warp_user /home/warp_user/warp/
RUN chgrp -R warp_user /home/warp_user/warp/

# Grant sudo access without password
RUN echo 'warp_user ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers

# Switch to the new user
WORKDIR /home/warp_user
USER warp_user

# This is needed to get around a bug in openmpi that would print copious error messages
# Unfortunately, this turns off CMA and uses shared memory for communication.
# An alternative is to do "docker run --cap-add SYS_PTRACE ...", which keeps CMA.
#ENV OMPI_MCA_btl_vader_single_copy_mechanism none

# Prepare the run directory
RUN mkdir run/
WORKDIR /home/warp_user/run/

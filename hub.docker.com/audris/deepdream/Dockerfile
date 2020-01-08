#  Modified to  support LDAP and be usable in the FDAC17 by Audris Mockus
# Based on google code

FROM ubuntu:trusty

RUN mkdir /deepdream
WORKDIR /deepdream


RUN apt-get -q update && \
  apt-get install --no-install-recommends -y --force-yes -q \
    openssh-server \
	     lsof sudo \
		  zsh \
		  libssl-dev \
		  sssd \
		  sssd-tools \
		  libnss-sss \
		  libpam-pwquality \
		  libpam-sss \
		  libsss-sudo \
		  ldap-utils \
		  vim \
		  build-essential \
    ca-certificates \
    git bc \
    python python-pip \
    python-dev libpython-dev \
    python-numpy python-scipy python-imaging \
    ipython ipython-notebook \
    libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev libboost-all-dev \
    libopenblas-dev libatlas-dev libatlas-base-dev libgflags-dev libgoogle-glog-dev liblmdb-dev protobuf-compiler && \
  apt-get clean && \
  rm /var/lib/apt/lists/*_*


# Download and compile Caffe
RUN git clone https://github.com/BVLC/caffe
RUN cd caffe && \
  cp Makefile.config.example Makefile.config && echo "CPU_ONLY := 1" >> Makefile.config && \
  make all -j2 
RUN pip install -U pip
RUN pip install cython jupyter
RUN cd caffe && \
  pip install --requirement python/requirements.txt 
RUN cd caffe && make pycaffe -j2
RUN cd caffe && make distribute
RUN cd caffe/scripts && ./download_model_binary.py ../models/bvlc_googlenet/

RUN pip install protobuf && pip install tornado --upgrade
RUN pip install numpy --upgrade
RUN apt-get -q update && \
  apt-get install --no-install-recommends -y --force-yes -q \
    python-jsonschema && \
  apt-get clean && \
  rm /var/lib/apt/lists/*_*

RUN git clone https://github.com/google/deepdream

# Uncomment to include DeepDream Video
RUN git clone https://github.com/graphific/DeepDreamVideo
RUN cd DeepDreamVideo && chmod a+x *.py

ENV LD_LIBRARY_PATH=/deepdream/caffe/distribute/lib
ENV PYTHONPATH=/deepdream/caffe/distribute/python

EXPOSE 8888

COPY eecsCA_v3.crt /etc/ssl/ 
COPY sssd.conf /etc/sssd/ 
COPY common* /etc/pam.d/ 
RUN chmod 0600 /etc/sssd/sssd.conf /etc/pam.d/common* 
RUN if [ ! -d /var/run/sshd ]; then mkdir /var/run/sshd; chmod 0755 /var/run/sshd; fi
COPY init.sh startsvc.sh startshell.sh notebook.sh startDef.sh /bin/ 
RUN ln /dev/null /dev/raw1394

ENV NB_USER jovyan
ENV NB_UID 1000
ENV HOME /home/$NB_USER
RUN useradd -m -s /bin/bash -N -u $NB_UID $NB_USER && mkdir $HOME/.ssh && chown -R $NB_USER:users $HOME 
RUN chown -R $NB_USER:users $HOME && chmod -R og-rwx $HOME/.ssh

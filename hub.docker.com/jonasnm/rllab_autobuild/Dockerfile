FROM ubuntu:16.04

# ========== Anaconda ==========
# https://github.com/ContinuumIO/docker-images/blob/master/anaconda/Dockerfile
RUN apt-get update --fix-missing && apt-get install -y wget bzip2 ca-certificates \
    libglib2.0-0 libxext6 libsm6 libxrender1 \
    git mercurial subversion
RUN echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh && \
    wget  --no-check-certificate --quiet https://repo.continuum.io/archive/Anaconda2-2.5.0-Linux-x86_64.sh && \
    /bin/bash /Anaconda2-2.5.0-Linux-x86_64.sh -b -p /opt/conda && \
    rm /Anaconda2-2.5.0-Linux-x86_64.sh

RUN apt-get install -y curl grep sed dpkg && \
    TINI_VERSION=`curl https://github.com/krallin/tini/releases/latest | grep -o "/v.*\"" | sed 's:^..\(.*\).$:\1:'` && \
    curl -L "https://github.com/krallin/tini/releases/download/v${TINI_VERSION}/tini_${TINI_VERSION}.deb" > tini.deb && \
    dpkg -i tini.deb && \
    rm tini.deb && \
    apt-get clean

ENV PATH /opt/conda/bin:$PATH
# http://bugs.python.org/issue19846
# > At the moment, setting "LANG=C" on a Linux system *fundamentally breaks Python 3*, and that's not OK.
ENV LANG C.UTF-8
ENTRYPOINT [ "/usr/bin/tini", "--" ]

# ========== Special Deps ==========
RUN apt-get -y install git make cmake unzip swig build-essential zlib1g-dev
RUN pip install awscli
# ALE requires zlib
# MUJOCO requires graphics stuff (Why?)
RUN apt-get -y build-dep glfw python-scipy
RUN apt-get -y install libxrandr2 libxinerama-dev libxi6 libxcursor-dev
# copied from requirements.txt
#RUN pip install imageio tabulate nose
RUN apt-get install -y vim ack-grep
RUN pip install --upgrade pip
# usual pip install pygame will fail
RUN apt-get build-dep -y python-pygame
RUN pip install Pillow

# ========== OpenAI Gym ==========
RUN apt-get -y install libgtk2.0-0
#RUN apt-get -y install ffmpeg
RUN apt-get -y install libav-tools
CMD alias ffmpeg="avconv"

# ========== GIT: OpenAI Gym and RLLAB ==========
CMD mkdir /root/code
CMD mkdir /root/git

RUN git clone https://github.com/jonasnm/rllab.git /root/git/rllab
RUN git clone -b jonas-experimental https://github.com/jonasnm/gym.git /root/git/gym


ENV PYTHONPATH /root/git/rllab:$PYTHONPATH
ENV PATH /opt/conda/envs/rllab3/bin:$PATH

#RUN echo "source activate rllab3" >> /root/.bashrc
#ENV BASH_ENV /root/.bashrc
#RUN ./root/git/rllab/scripts/setup_linux.sh
RUN pip install -e /root/git/gym/
WORKDIR /root/code

# cpu theano
ENV THEANO_FLAGS mode=FAST_RUN,device=cpu,floatX=float32

# Downgrading Lasagne due to theano compatibility issue
run pip install --upgrade https://github.com/Lasagne/Lasagne/archive/master.zip

COPY ./conda_script.sh /root/code/
RUN chmod +x /root/code/conda_script.sh
RUN /root/code/conda_script.sh

# Changing to nomkl
#RUN conda install nomkl numpy scipy scikit-learn numexpr
#RUN conda remove mkl mkl-service

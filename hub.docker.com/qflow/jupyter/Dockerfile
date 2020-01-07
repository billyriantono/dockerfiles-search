FROM nvidia/cuda:8.0-cudnn5-devel-ubuntu16.04
MAINTAINER Michal Fojtak <mfojtak@seznam.cz>
RUN apt-get update && apt-get install -y software-properties-common && add-apt-repository -y ppa:jonathonf/ffmpeg-3 && \
    apt-get update && apt-get install -y --no-install-recommends ffmpeg libavfilter-dev libavdevice-dev libavcodec-dev libav-tools x264 x265 && \
    apt-get install -y libopencv-dev python-opencv iputils-ping nano cifs-utils wget
########## REQUIRED DEPENDENCIES ################
RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
    build-essential \
    cmake \
    libprotobuf-dev \
    protobuf-compiler \
    libgoogle-glog-dev

#RUN git clone --recursive --branch v0.7.0 https://github.com/caffe2/caffe2.git

########## OPTIONAL DEPENDENCIES ################

#RUN apt-get install -y --no-install-recommends \
#    libgflags-dev \
#    libgoogle-glog-dev \
#    libgflags-dev \
#    libgtest-dev \
#    libiomp-dev \
#    libleveldb-dev \
#    liblmdb-dev \
#    libopenmpi-dev \
#    libsnappy-dev \
#    openmpi-bin \
#    openmpi-doc \
#    python-numpy \
#    python-pydot \
#    python-setuptools \
#    python-scipy 
    
RUN echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh && \
    wget --quiet https://repo.continuum.io/archive/Anaconda2-4.4.0-Linux-x86_64.sh -O ~/anaconda.sh && \
    /bin/bash ~/anaconda.sh -b -p /opt/conda && \
    rm ~/anaconda.sh
ENV PATH /opt/conda/bin:$PATH
RUN conda install opencv numba bokeh accelerate libgcc wget && conda install -c conda-forge jupyter_contrib_nbextensions jupyter_nbextensions_configurator
RUN pip install av jupyter-git tensorflow-gpu

########## INSTALLATION STEPS ###################
#RUN cd caffe2 && make -j4 && cd build && make -j4 install

#ENV PYTHONPATH /usr/local
#ENV LD_LIBRARY_PATH /usr/local/lib:$LD_LIBRARY_PATH
#ENV LIBRARY_PATH /usr/local/lib:$LD_LIBRARY_PATH
#RUN python -c 'from caffe2.python import core' 2>/dev/null && echo "Success" || echo "Failure"

ADD video.ipynb /tutorials/video/video.ipynb
ADD motion.ipynb /tutorials/video/motion.ipynb
ADD test.ipynb /tutorials/video/test.ipynb
ADD small.mp4 /tutorials/video/small.mp4
ADD jupyter_notebook_config.py /root/.jupyter/
ADD start.sh /start.sh
RUN chmod +x /start.sh
EXPOSE 8888
ENTRYPOINT ["/start.sh"]

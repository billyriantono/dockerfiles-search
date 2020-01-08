FROM nvidia/cuda:10.0-cudnn7-devel-ubuntu18.04

LABEL maintainer sminamino

ARG JUPYTER_PASSWORD="sakurayutakao-"
ARG USER_NAME="yamanoshiragiku"
ARG USER_PASSWORD="mrcb"

SHELL ["/bin/bash", "-c"]

# Set environment
ENV TERM xterm
ENV LC_ALL=C.UTF-8
ENV LANG C.UTF-8
# timezone setting
ENV TZ=Asia/Tokyo

ENV DEBIAN_FRONTEND=noninteractive

RUN DEBIAN_FRONTEND=noninteractive \
    apt-get update -y && apt-get install -y --no-install-recommends \
    apt-utils \
    less \
    wget \
    curl \
    git \
    graphviz \
    unzip \
    bzip2 \
    build-essential \
    vim \
    libncursesw5-dev \
    libgdbm-dev \
    libc6-dev \
    zlib1g-dev \
    libsqlite3-dev \
    tk-dev \
    libssl-dev \
    openssl \
    libbz2-dev \
    libreadline-dev \
    cmake

COPY ./autokeras-0.4.0.tar.gz /tmp/autokeras-0.4.0.tar.gz

# Install Anaconda
RUN wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh && /bin/bash ~/miniconda.sh -b -p ~/conda && rm ~/miniconda.sh

ENV PATH $PATH:/root/conda/bin/

RUN conda install -y conda

RUN conda create -n ML python=3.6 anaconda

RUN conda install -y notebook ipykernel

RUN ipython kernel install --user --name=ML --display-name=ML

RUN conda install -y \
  numpy \
  scipy \
  scikit-learn \
  jupyter \
  notebook \
  ipython \
  tensorflow-gpu

# install LightGBM and XGBoost
RUN conda install -c conda-forge lightgbm xgboost

#RUN git clone --recursive https://github.com/Microsoft/LightGBM && \
#cd LightGBM/python-package &&\
#python setup.py install

#RUN git clone --recursive https://github.com/microsoft/LightGBM ; cd LightGBM
#RUN mkdir build ; cd build
#RUN cmake ..
#RUN make -j4

RUN conda install -c conda-forge lightgbm

ENV NOTO_DIR /usr/share/fonts/opentype/notosans
RUN mkdir -p ${NOTO_DIR} &&\
  wget -q https://noto-website-2.storage.googleapis.com/pkgs/NotoSansCJKjp-hinted.zip -O noto.zip &&\
  unzip ./noto.zip -d ${NOTO_DIR}/ &&\
  chmod a+r ${NOTO_DIR}/NotoSans* &&\
  rm ./noto.zip

RUN source activate ML &&\
  conda install pip &&\
  conda install -c conda-forge julia &&\
  pip install tensorflow-gpu \
  numpy \
  scipy \
  scikit-learn \
  torch torchvision \
  ipython &&\
  conda install -c conda-forge lightgbm &&\
  pip install git+git://github.com/keras-team/autokeras@master

CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--port=8888", "--allow-root"]

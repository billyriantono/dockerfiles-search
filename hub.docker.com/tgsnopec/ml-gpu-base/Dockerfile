FROM nvidia/cuda:10.0-cudnn7-devel-ubuntu16.04

ARG PYTHON_VERSION=3.6

# Install dependencies
RUN apt-get update
RUN apt-get install -y --no-install-recommends \
            apt-utils \
            bc \
            build-essential \
            cmake \
            curl \
            g++ \
            gfortran \
            git \
            libffi-dev \
            liblapack-dev \
            pkg-config \
            wget
RUN apt-get clean
RUN apt-get autoremove
RUN rm -rf /var/lib/apt/lists/*

# PyTorch recommends installation through conda
RUN curl -o ~/miniconda.sh -O https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
RUN chmod +x ~/miniconda.sh
RUN ~/miniconda.sh -b -p /opt/conda
RUN rm ~/miniconda.sh
RUN /opt/conda/bin/conda install -y python=$PYTHON_VERSION numpy pyyaml scipy mkl mkl-include cython typing
RUN /opt/conda/bin/conda install scikit-learn pandas nose
RUN /opt/conda/bin/conda install pytorch torchvision cudatoolkit=10.0 -c pytorch
RUN /opt/conda/bin/conda clean -ya

ENV PATH /opt/conda/bin:$PATH

CMD ["/bin/bash"]

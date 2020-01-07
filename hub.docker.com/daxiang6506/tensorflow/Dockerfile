FROM daxiang6506/anaconda3:5.1.0

COPY requirements.txt .

COPY run_jupyter.sh /

RUN conda update -n base conda && \
    conda create --name tf python=3.6 && \
    /bin/bash -c 'source /opt/conda/bin/activate tf && \
    pip install -r requirements.txt' && \
    echo "conda activate tf" >> ~/.bashrc

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    libgtk2.0-dev \
    libav-tools

RUN apt-get update && \
    apt-get install -y \
    git \
    python-pip \
    python-numpy \
    python-dev \
    cmake \
    zlib1g-dev \
    libjpeg-dev \
    xvfb \
    libav-tools \
    xorg-dev \
    python-opengl \
    libboost-all-dev \
    libsdl2-dev \
    swig

RUN chmod 777 /run_jupyter.sh 

WORKDIR /root/notebook

# TensorBoard
EXPOSE 6006
# IPython
EXPOSE 8888
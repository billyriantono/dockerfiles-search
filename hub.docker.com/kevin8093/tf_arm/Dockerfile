FROM arm32v7/ubuntu:16.04

LABEL mantainer="Kevin Zhao <kevin8093@126.com>"
RUN sed -i 's/http:\/\/archive\.ubuntu\.com\/ubuntu\//http:\/\/mirrors\.163\.com\/ubuntu\//g' /etc/apt/sources.list
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    curl \
    libfreetype6-dev \
    libpng12-dev \
    libzmq3-dev \
    pkg-config \
    python \
    python-dev \
    python-tk \
    rsync \
    software-properties-common \
    unzip \
    git \
    && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN curl -O https://bootstrap.pypa.io/get-pip.py && \
    python get-pip.py && \
        rm get-pip.py

RUN pip --no-cache-dir install \
     Pillow \
     h5py \
     ipykernel \
     jupyter \
     matplotlib \
     numpy \
     pandas \
     scipy \
     sklearn \
     && \
     python -m ipykernel.kernelspec

ADD tensorflow-1.3.0-cp27-none-linux_armv7l.whl .

RUN pip --no-cache-dir install tensorflow-1.3.0-cp27-none-linux_armv7l.whl && \
    rm -f tensorflow-1.3.0-cp27-none-linux_armv7l.whl

COPY jupyter_notebook_config.py /root/.jupyter/

# Copy sample notebooks.
COPY notebooks /notebooks

# Jupyter has issues with being run directly:
#   https://github.com/ipython/ipython/issues/7062
# We just add a little wrapper script.
COPY run_jupyter.sh /
RUN chmod +x /run_jupyter.sh

# TensorBoard
EXPOSE 6006
# IPython
EXPOSE 8888

WORKDIR "/notebooks"

CMD ["/run_jupyter.sh", "--allow-root"]

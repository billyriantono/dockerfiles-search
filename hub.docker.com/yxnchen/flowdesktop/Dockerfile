FROM consol/ubuntu-xfce-vnc

USER 0

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
ENV PATH /opt/conda/bin:$PATH

RUN apt-get update --fix-missing && \
    apt-get install -y wget bzip2 ca-certificates libglib2.0-0 libxext6 \
    libsm6 libxrender1 git mercurial subversion && \
    rm -rf /var/lib/apt/lists/*

RUN wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-4.5.4-Linux-x86_64.sh -O ~/miniconda.sh && \
    /bin/bash ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh && \
    ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh && \
    echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc && \
    echo "conda activate base" >> ~/.bashrc

ADD https://github.com/krallin/tini/releases/download/v0.18.0/tini /usr/bin/tini
RUN chmod +x /usr/bin/tini
# RUN apt-get -o Acquire::http::No-Cache=True -o Acquire::http::Pipeline-Depth=0 install -y curl \
#     grep sed dpkg && \
#     TINI_VERSION=`curl https://github.com/krallin/tini/releases/latest | grep -o "/v.*\"" | sed 's:^..\(.*\).$:\1:'` && \
#     curl -L "https://github.com/krallin/tini/releases/download/v${TINI_VERSION}/tini_${TINI_VERSION}.deb" > tini.deb && \
#     dpkg -i tini.deb && \
#     rm tini.deb && \
#     apt-get clean

RUN apt-get update --fix-missing && apt-get upgrade -y && \
    apt-get install -y cmake swig libgtest-dev python-pygame python-scipy autoconf libtool pkg-config libgdal-dev libxerces-c-dev && \
    apt-get install -y  libproj-dev libfox-1.6-dev libxml2-dev libxslt1-dev build-essential curl unzip flex bison python python-dev python3-dev && \
    rm -rf /var/lib/apt/lists/*

RUN pip --no-cache-dir install --upgrade pip setuptools && \
    conda update -n base conda && \
    pip --no-cache-dir install cmake cython

# install Flow and SUMO
RUN cd ~ && git clone https://github.com/flow-project/flow.git && \
    cd flow && \
    git checkout v0.3.0 && \
    conda env create -f environment.yml && \
    python setup.py develop && \
    echo 'export PYTHONPATH="$HOME/flow:$PYTHONPATH"' >> ~/.bashrc && \
    ./scripts/setup_sumo_ubuntu1604.sh

# install Rllab
RUN cd ~ && \
    git clone https://github.com/cathywu/rllab-multiagent.git && \
    cd rllab-multiagent && \
    conda env create -f environment.yml && \
    python setup.py develop && \
    echo 'export PYTHONPATH="$HOME/rllab-multiagent:$PYTHONPATH"' >> ~/.bashrc

RUN echo "source activate flow" >> /root/.bashrc && \
    echo "source activate flow"
ENV BASH_ENV /root/.bashrc

# install SUMO
# RUN cd ~/flow && \
#     ./scripts/setup_sumo_ubuntu1604.sh && \
#     echo 'export SUMO_HOME="$HOME/sumo"' >> ~/.bashrc && \
#     echo 'export PATH="$HOME/sumo/bin:$PATH"' >> ~/.bashrc && \
#     echo 'export PYTHONPATH="$HOME/sumo/tools:$PYTHONPATH"' >> ~/.bashrc

##  RAY
RUN apt-get update && \
    apt-get install -y libboost-dev libboost-test-dev libboost-program-options-dev libboost-filesystem-dev \
    libboost-thread-dev libevent-dev automake libtool flex bison pkg-config g++ libssl-dev && \
    rm -rf /var/lib/apt/lists/*
RUN git clone https://github.com/apache/thrift && \
    cd thrift && \
    ./bootstrap.sh && \
    ./configure && make && make install

#### RAY 
RUN cd ~ && conda install libgcc jupyter && \
    apt-get update && \
    apt-get install -y cmake pkg-config build-essential autoconf curl libtool libboost-dev libboost-filesystem-dev libboost-system-dev unzip bison openssl && \
    rm -rf /var/lib/apt/lists/* && \
    git clone https://github.com/eugenevinitsky/ray && \
    cd ray/python && python setup.py develop && \
    echo 'export PYTHONPATH="$HOME/flow:$PYTHONPATH"' >> ~/.bashrc && \
    pip --no-cache-dir install lz4 gym==0.10.5

USER 0

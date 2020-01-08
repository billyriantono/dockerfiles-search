FROM ubuntu:16.04

# Install dependencies
RUN apt-get update
RUN apt-get install -y \
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
            python3-dev \
            python3-numpy \
            python3-pip \
            python3-tk \
            wget
RUN apt-get clean
RUN apt-get autoremove
RUN rm -rf /var/lib/apt/lists/*

# Install other useful Python packages using pip
RUN pip3 install --upgrade pip
RUN pip3 --no-cache-dir install \
                        joblib>=0.13.1 \
                        lasio>=0.23 \
                        matplotlib \
                        nose \
                        numpy==1.16.1 \
                        pandas>=0.20.3 \
                        pyyaml \
                        pytest>=3.2.0\
                        scikit-learn>=0.20.2 \
                        scipy==1.2.0 \
                        tqdm>=4.15.0 \
                        xgboost==0.81 \
                        zmq

# Install from source
RUN pip3 install --no-binary :all: lightgbm==2.2.3

RUN apt-get autoremove

CMD ["/bin/bash"]


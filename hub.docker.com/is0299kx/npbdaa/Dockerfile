#Docker image for Nonparametric Bayesian Double Articulation Analyzer

#Pull the official image
FROM ubuntu:16.04

#Install dependencies
RUN apt-get update -y && apt-get install -y --no-install-recommends \
    ca-certificates \
    gcc \
    git \
    g++ \
    libbz2-dev \
    libssl-dev \
    make \
    tk-dev \
    wget \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

#Install Python-3.6.5
RUN wget https://www.python.org/ftp/python/3.6.5/Python-3.6.5.tgz \
 && tar zxf Python-3.6.5.tgz \
 && cd Python-3.6.5 \
 && ./configure \
 && make altinstall \
 && make clean \
 && cd .. \
 && rm -rf Python-3.6.5.tgz \
    Python-3.6.5

#Install requirements
RUN yes | pip3.6 --no-cache-dir install \
    numpy==1.14.2 \
    scipy==1.0.1 \
    cython==0.28.2 \
    joblib==0.11 \
    matplotlib==2.2.2 \
    scikit-learn==0.19.1 \
    tqdm==4.23.4

#Install pybasicbayes
RUN git clone https://github.com/mattjj/pybasicbayes git_work \
 && cd git_work \
 && python3.6 setup.py install \
 && cd .. \
 && rm -rf git_work

#Install pyhsmm
RUN git clone https://github.com/mattjj/pyhsmm git_work \
 && cd git_work \
 && python3.6 setup.py install \
 && cd .. \
 && rm -rf git_work

#Install pyhlm
WORKDIR /root/
RUN git clone https://github.com/RyoOzaki/npbdaa npbdaa \
 && cd npbdaa \
 && python3.6 setup.py install \
 && cd ..

#Set backend
RUN mkdir -p .config/matplotlib \
 && touch .config/matplotlib/matplotlibrc \
 && echo 'backend : Agg' >> .config/matplotlib/matplotlibrc

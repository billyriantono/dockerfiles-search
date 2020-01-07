FROM zyxue/linuxbrew
MAINTAINER alfred532008@gmail.com

RUN sudo apt-get install -y build-essential wget git

RUN set -x \
    && wget --no-check-certificate "https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-4.0.0-Linux-x86_64.sh" \
    && bash  Anaconda3-4.0.0-Linux-x86_64.sh -b \
    && rm -v Anaconda3-4.0.0-Linux-x86_64.sh

ENV PATH /home/linuxbrew/anaconda3/bin:$PATH

RUN conda install -y ipython pandas matplotlib scikit-learn

RUN git clone --recursive https://github.com/dmlc/xgboost \
    && cd xgboost && make \
    && cd python-package && python setup.py install \
    && cd && rm -rf xgboost

# needed by import matplotlib.pyplot as plt
RUN sudo apt-get install -y libglib2.0-0 libsm6 qt4-default

RUN conda install -y seaborn

# https://github.com/benhamner/Metrics/tree/master/Python
RUN pip install ml_metrics

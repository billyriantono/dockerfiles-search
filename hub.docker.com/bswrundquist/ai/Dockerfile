FROM anibali/pytorch:cuda-10.0

USER root 

RUN apt-get update && apt-get install -y \
    wget \
    vim \
    build-essential

# RUN  conda update -n base conda

RUN conda update numpy
RUN pip install -U pip
RUN pip install Cython

RUN conda install --quiet --yes \
    'plotly' \
    'seaborn' \
    'pandas'

RUN pip install scikit-optimize

RUN pip install more_itertools 

RUN pip install sphinx \
    pytest

RUN apt-get install -y gcc

RUN pip install lime 

RUN conda install pyyaml mkl mkl-include setuptools cmake cffi typing numba numexpr

#RUN pip install pyro-ppl \
#    gym[atari]

RUN pip install deap

RUN pip install JayDeBeApi \
    pymssql
USER root        
RUN apt-get update       
RUN apt-get install -y default-jre

RUN pip install pyDOE
RUN pip install Faker

RUN pip install cryptography \
    pycryptodomex

RUN conda install -c conda-forge hdbscan

RUN pip install papermill
RUN pip install filterpy
RUN pip install fbprophet

RUN pip install tensorflow \
    tensorboardX

RUN pip install fire==0.1.3
RUN pip install gym==0.10.5

RUN pip install python-jenkins
RUN pip install ruamel.yaml

RUN conda install pyarrow -c conda-forge
RUN pip install feather-format

RUN pip install jsonnet

RUN pip install xgboost

RUN pip uninstall -y numpy
RUN pip uninstall -y numpy 
RUN pip uninstall -y numpy  # multiple version for some reason?... 

RUN pip install numpy

RUN conda install --channel conda-forge --yes boost boost-cpp pyarrow

RUN pip install ruamel.yaml
RUN pip install scikit-optimize



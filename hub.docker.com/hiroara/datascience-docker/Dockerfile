FROM ubuntu:14.04

MAINTAINER Hiroki Arai <hiroara62@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

# Install packages
RUN apt-get -y update && apt-get install -y wget nano locales curl unzip wget openssl libhdf5-dev

ENV LANGUAGE en_US.UTF-8
ENV LANG en_US.UTF-8

RUN locale-gen en_US.UTF-8
RUN dpkg-reconfigure locales

# Install the POSTGRES package so we can connect to Postres servers if need be
RUN apt-get install -y libpq-dev

# Install and setup minimal Anaconda Python distribution
RUN wget http://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -O miniconda.sh
RUN bash miniconda.sh -b -p /anaconda && rm miniconda.sh
ENV PATH /anaconda/bin:$PATH

# Set the time zone to the local time zone
RUN echo "America/Los_Angeles" > /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata

# For image inheritance.
ONBUILD ENV PATH /anaconda/bin:$PATH

# Install some essential data science packages in python, including psycopg2
RUN conda install scipy numpy scikit-learn scikit-image pyzmq nose readline pandas matplotlib seaborn dateutil ipython-notebook nltk pip
RUN conda install psycopg2
RUN conda install cython hdf5 pytables


# Get plotly
RUN pip install plotly

# get all the nltk data
RUN python -m nltk.downloader all

# Get the latest gensim
RUN pip install gensim==0.11.1

# Get the latest Theano
RUN pip install Theano

# Install mecab and these python module
RUN apt-get install -y g++ mecab libmecab-dev mecab-ipadic-utf8 && pip install mecab-python3

# Install git-core
RUN apt-get install -y git-core

# Install Pylearn2
RUN git clone git://github.com/lisa-lab/pylearn2.git && cd pylearn2 && python setup.py develop

ENV PEM_FILE /key.pem
# $PASSWORD will get `unset` within notebook.sh, turned into an IPython style hash
ENV PASSWORD Dont make this your default
ENV USE_HTTP 1

# Add current files to / and set entry point.
ADD . /workspace
WORKDIR /workspace
ADD notebook.sh /notebook.sh
RUN chmod a+x /notebook.sh

EXPOSE 8888

CMD ["/notebook.sh"]


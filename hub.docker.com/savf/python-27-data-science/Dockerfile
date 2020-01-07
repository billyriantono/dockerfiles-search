FROM python:2.7

MAINTAINER Stephan Mannhart

RUN apt-get update && apt-get install -y \
    gfortran \
    # needed for shapely
    libgeos-c1 libgeos-dev \
    libpq-dev \
    libblas-dev liblapack-dev \
    libmysqlclient-dev \
    python-dev \
	libfreetype6-dev \
	libpng-dev
RUN rm -rf /var/lib/apt/lists/*
RUN ln -s /usr/include/freetype2/ft2build.h /usr/include/

# Install pandas/ numpy / scipy / scikit-learn and their deps
RUN pip install six==1.10.0 \
 numpy==1.12.1 \
 scipy==0.19.0 \
 scikit-learn==0.18.1 \
 nltk==3.2.4
 
 # Install the stopwords corpora and the punkt tokenizer
RUN python -m nltk.downloader 'stopwords'
RUN python -m nltk.downloader 'punkt'

RUN pip install pandas==0.20.1

RUN pip install Flask==0.12.2 \
 Flask-RESTful==0.3.6 \
 pytz==2017.2 \
 pyzmq==16.0.2 \
 rethinkdb==2.3.0.post6 \
 requests==2.13.0

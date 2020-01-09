# Dockerfile for gwas_base
# Version 0.1

FROM google/python
MAINTAINER Uemit Seren <uemit.seren@gmail.com>

# compilers and basic tools
RUN apt-get update -y && apt-get install --no-install-recommends -y -q build-essential gfortran make gcc git-core python-imaging libpng-dev libfreetype6 libfreetype6-dev curl

# hdf5
ADD hdf5_install.sh /tmp/hdf5_install.sh
RUN sh /tmp/hdf5_install.sh

#openblas
ADD openblas_install.sh /tmp/openblas_install.sh
RUN sh /tmp/openblas_install.sh

# blas
ENV BLAS /usr/local/lib/libopenblas.a

# lapack
ENV LAPACK /usr/local/lib/libopenblas.a

#LD path
ENV LD_LIBRARY_PATH $LD_LIBRARY_PATH:/usr/local/lib/

WORKDIR /app

# Create environment 
RUN virtualenv /env

#Install numpy first because otherwise matplotlib, tables and numexpr fail (https://github.com/pypa/pip/issues/720)
RUN /env/bin/pip install numpy>=1.9.1

# Add requirement file
ADD requirements.txt /app/requirements.txt
RUN /env/bin/pip install -r requirements.txt

RUN apt-get autoremove -y && apt-get clean -y

CMD ["bash"]

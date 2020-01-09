##############################################################################################
# Purpose   : Docker images of PSS to SDP send/receive data pipeline
# Python    : 3.6
# Version   : 1.1
# Author    : Benjamin Shaw (benjamin.shaw@manchester.ac.uk)
##############################################################################################

# This docker file will set up an environment with some python3.6
# and some other basic tools for reading filterbank files
# and implementing UDP data transfer capabilities with spead2

# SOFTWARE:

# 1. python 3.6
# 2. pip
# 3. spead2
# 4. filtools
# ...and associated dependencies

# Import distribution
FROM centos:8

# Set labels
LABEL maintainer="Benjamin Shaw"
LABEL description="This dockerfile implements the spead2 UDP data transfer library"

# The WORKDIR instruction sets the working directory for any RUN, CMD, ENTRYPOINT,
# COPY and ADD instructions that follow it in the Dockerfile. If the WORKDIR doesn’t
# exist, it will be created even if it’s not used in any subsequent Dockerfile instruction.
WORKDIR /home

#################################################################
# Install packages and dependencies from system package manager #
#################################################################
RUN yum -y install \
    # python3-devel is a package that 
    # allows one to build python extensions
    # This is a dependency for spead2 
    python3-devel \
    # python3-pip is a package manager for 
    # python
    python3-pip \
    # gcc-c++ is a GNU compiler for C++
    # This is a dependency of spead2
    gcc-c++ \
    # boost-devel is a set of C++ source libraries
    # and is a dependency of spead2
    boost-devel \
    # Git: for installing filtools and send/receive
    git 

###########################
# Install spead2 from pip #
###########################
RUN pip3 install --no-cache-dir spead2

###############################################
# Install filtools, scipy and yaml from pip   #
# filtools is a set of tools for              #
# reading and writing filterbank files        #
###############################################
RUN pip3 install --no-cache-dir git+https://bitbucket.org/mkeith/filtools && \
    pip3 install --no-cache-dir scipy && \
    pip3 install --no-cache-dir pyyaml

# Define the commands that will be run when the container is created
WORKDIR /home
ENTRYPOINT /bin/bash

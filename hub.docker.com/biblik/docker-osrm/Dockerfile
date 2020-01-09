FROM ubuntu:14.04

MAINTAINER biblik <axel.grimault@gmail.com>

# UPDATE PACKAGES
RUN apt-get -y update

# INSTALL REQUIRED PACKAGES FOR OSRM-BACKEND
RUN apt-get -y install build-essential git cmake pkg-config
RUN apt-get -y install libbz2-dev libzip-dev libxml2-dev
RUN apt-get -y install libstxxl-dev libstxxl-doc libstxxl1 
RUN apt-get -y install libboost-all-dev
RUN apt-get -y install lua5.1 liblua5.1-0-dev libluabind-dev libluajit-5.1-dev
RUN apt-get -y install libtbb-dev

# INSTALL OSRM-BACKEND
WORKDIR /opt/osrm
RUN git clone https://github.com/Project-OSRM/osrm-backend.git
WORKDIR /opt/osrm/osrm-backend
RUN git checkout master
RUN mkdir -p build
WORKDIR /opt/osrm/osrm-backend/build
RUN cmake ..
RUN make

# PREPARE PROFILE DIRECTORY
WORKDIR /opt/osrm/
RUN mkdir -p profile

# PREPARE DATA DIRECTORY
WORKDIR /opt/osrm/
RUN mkdir -p data

VOLUME ["/opt/osrm/data","/opt/osrm/profile"]

# PREPARE OSRM
WORKDIR /opt/osrm/
RUN mkdir -p stxxl
WORKDIR /opt/osrm/osrm-backend/build/
RUN echo 'disk=/opt/osrm/stxxl/stxxl,25000,syscall' > .stxxl

# RUN SCRIPT
WORKDIR /opt/osrm/
ADD install.sh /opt/osrm/install.sh
RUN chmod 700 install.sh
CMD ./install.sh

EXPOSE 5000

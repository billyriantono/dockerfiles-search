FROM 32bit/debian:jessie
MAINTAINER Mirko Weber <mirko.weber@gmail.com>

RUN apt-get update
RUN apt-get install -yq build-essential debootstrap python-pip automake \
  libgmp3-dev libltdl-dev libunistring-dev libffi-dev imagemagick libssl-dev \
  pkg-config zlib1g-dev gettext git curl subversion check intltool gperf flex \
  bison xmlto php5 expect libgc-dev mercurial cython lzip cmake swig \
  libboost1.55-tools-dev libncurses5-dev vim
RUN pip install -U setuptools pip==1.5.4 wheel==0.23 httpie
RUN mkdir -p /spksrc
WORKDIR /spksrc

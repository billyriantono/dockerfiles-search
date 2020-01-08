FROM continuumio/anaconda3
RUN echo "Installing Essential dependencies..."
RUN apt-get -y update
RUN apt-get -y install build-essential
RUN apt-get -y install llvm
RUN apt-get -y install clang libc++-dev libc++abi-dev
RUN apt-get -y install cmake
RUN apt-get -y install git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev
RUN apt-get -y install libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libjasper-dev libdc1394-22-dev checkinstall cpio axel build-essential
RUN apt-get -y install s3cmd p7zip-full

RUN conda install -y cmake gcc boost
RUN conda install -y jupyter
RUN conda install -y -c conda-forge xgboost 
RUN conda install -y -c conda-forge libarchive 
RUN conda install -y -c conda-forge python-libarchive-c 

RUN pip install pandas_ml
RUN pip install luigi

FROM kmubigdata/ubuntu-cuda-cudnn

MAINTAINER kmubigdata <bigdata.cs.kookmin.ac.kr>

# Install OPENCV
RUN apt-get update \
		&& apt-get upgrade -y \
		&& apt-get install -y unzip wget build-essential \
			cmake git pkg-config libswscale-dev \
			python3-dev python3-numpy \
			python2.7-dev \
			libtbb2 libtbb-dev libjpeg-dev \
			libpng-dev libtiff-dev libjasper-dev
RUN cd \
		&& wget https://github.com/opencv/opencv/archive/3.2.0.zip \
		&& unzip 3.2.0.zip \
		&& cd opencv-3.2.0 \
		&& mkdir build \
		&& cd build \
		&& cmake .. \
		&& make -j8 \
		&& make install \
		&& cd \
		&& rm 3.2.0.zip

# Install Tensorflow-gpu
RUN apt-get update
RUN apt-get install -y libcupti-dev
RUN wget https://bootstrap.pypa.io/get-pip.py
RUN apt-get -y install python
RUN python get-pip.py 
RUN apt-get install -y python-pip python-dev 
RUN pip install tensorflow-gpu
ENV LD_LIBRARY_PATH /usr/local/cuda-8.0/lib64/:${LD_LIBRARY_PATH}

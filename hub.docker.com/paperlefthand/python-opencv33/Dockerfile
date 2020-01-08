FROM debian:stretch

# ARG project_dir=/src/
# ADD src $project_dir

RUN apt-get update \
	&& apt-get install -y unzip wget build-essential \
		cmake git pkg-config apt-utils libswscale-dev \
		python3-dev python3-numpy python3-matplotlib \
		libtbb2 libtbb-dev libjpeg-dev \
		libpng-dev libtiff-dev \
	&& groupadd -r user \
	&& useradd -r -g user user

#    && chown -R user:user $project_dir

RUN cd \
	&& wget https://github.com/opencv/opencv/archive/3.3.0.zip \
	&& unzip 3.3.0.zip \
	&& cd opencv-3.3.0 \
	&& mkdir build \
	&& cd build \
	&& cmake .. \
	&& make -j3 \
	&& make install \
	&& cd \
	&& rm 3.3.0.zip

USER user

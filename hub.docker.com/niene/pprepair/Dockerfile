# Operating system image:
FROM ubuntu:16.04
MAINTAINER Niene Boeijen <niene@webmapper.net>

ENV BUILD_PACKAGES cmake wget git ca-certificates build-essential 
ENV GDAL_PACKAGES libgeos-c1v5 libgdal-dev gdal-bin libcgal-dev libcgal-demo
ENV DATA_DIR repair_files

# Create data directory
RUN mkdir -p $DATA_DIR

# Install dependencies CGAL GDAL CMake

RUN apt-get -qq update && apt-get -qq --yes upgrade \
	&& apt-get install -y $BUILD_PACKAGES --no-install-recommends

RUN echo "deb http://ppa.launchpad.net/ubuntugis/ubuntugis-unstable/ubuntu xenial main" > /etc/apt/sources.list.d/ubuntugis.list && \
	apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 314DF160 && \
	apt-get -qq -y update && apt-get install -qq -y $GDAL_PACKAGES 

RUN git clone https://github.com/tudelft3d/pprepair.git  && \
	cd pprepair && \
	sed -i '81 s/^/#/' CMakeLists.txt && \
	sed -i '82 s/#//' CMakeLists.txt && \
	cmake -DDRIVER="ESRI Shapefile" . && \
	make

# Set usr/bin/pprepair as the dockerized entry-point application
ENTRYPOINT ["/pprepair/pprepair"]

VOLUME $DATA_DIR
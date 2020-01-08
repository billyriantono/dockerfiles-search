FROM python:2.7
MAINTAINER Ohad Galor Kimchi <ohadgk@gmail.com>

ENV OCTOPRINT_VERSION=1.3.2
ENV CURA_ENGINE_VERSION=15.04.6

RUN set -xe \
	&& echo "Setup Temporary packages for compilation" \
	&& export PKGS='build-essential subversion libjpeg-dev zlib1g-dev libv4l-dev wget unzip git cmake' \
	&& echo "Installing Dependencies" \
	&& apt-get update \
	&& apt-get install -y libprotobuf10 libav-tools avrdude libjpeg62-turbo curl imagemagick psmisc --no-install-recommends \
	&& apt-get install -y ${PKGS} --no-install-recommends \
	&& echo "Download OctoPrint/CuraEngine/mjpg-streamer" \
	&& cd /tmp/ \
	&& wget https://github.com/Ultimaker/CuraEngine/archive/${CURA_ENGINE_VERSION}.tar.gz \
	&& wget https://github.com/jacksonliam/mjpg-streamer/archive/master.zip \
	&& echo "Installing mjpg-streamer" \
	&& unzip master.zip \
	&& cd mjpg-streamer-master/mjpg-streamer-experimental \
	&& make \
	&& make install \
	&& cd ../.. \
	&& echo "Installing CuraEngine" \
	&& tar -zxf ${CURA_ENGINE_VERSION}.tar.gz \
	&& cd CuraEngine-${CURA_ENGINE_VERSION} \
	&& mkdir build \
	&& make \
	&& mv -f ./build /CuraEngine/ \
	&& cd .. \
	&& echo "Cleaning Temporary Packages + Installation leftovers" \
	&& rm -rf /var/lib/apt/lists/* \
	&& rm -rf /tmp/* /var/tmp/*

RUN set -xe \
	&& cd /tmp/ \
	&& wget https://github.com/foosel/OctoPrint/archive/${OCTOPRINT_VERSION}.tar.gz \
	&& echo "Installing OctoPrint" \
	&& tar -zxf ${OCTOPRINT_VERSION}.tar.gz \
	&& mv -f OctoPrint-${OCTOPRINT_VERSION} /octoprint/ \
	&& cd /octoprint/ \
	&& echo "Install OctoPrint requirements" \
	&& pip install -r requirements.txt \
	&& pip install pillow \
	&& python setup.py install \
	&& rm -rf /tmp/* /var/tmp/*

VOLUME /data
WORKDIR /data

EXPOSE 5000
# TODO: Until i'll add HAProxy
EXPOSE 8088

ADD octoprint.sh /usr/bin/
ENV YUV_CAMERA "true"

ENTRYPOINT ["octoprint.sh"]
CMD []

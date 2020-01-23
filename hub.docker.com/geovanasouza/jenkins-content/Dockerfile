# =================================================================
#
# Authors: Just van den Broecke <justb4@gmail.com>
#
# Copyright (c) 2019 Just van den Broecke
#
# Permission is hereby granted, free of charge, to any person
# obtaining a copy of this software and associated documentation
# files (the "Software"), to deal in the Software without
# restriction, including without limitation the rights to use,
# copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the
# Software is furnished to do so, subject to the following
# conditions:
#
# The above copyright notice and this permission notice shall be
# included in all copies or substantial portions of the Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
# EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES
# OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
# NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT
# HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY,
# WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING
# FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR
# OTHER DEALINGS IN THE SOFTWARE.
#
# =================================================================

FROM debian:buster-slim

LABEL maintainer="Just van den Broecke <justb4@gmail.com>"

# ARGS
ARG TIMEZONE="Europe/London"
ARG LOCALE="en_US.UTF-8"
ARG ADD_DEB_PACKAGES=""
ARG ADD_PIP_PACKAGES=""

# ENV settings
ENV TZ=${TIMEZONE} \
	DEBIAN_FRONTEND="noninteractive" \
	DEB_BUILD_DEPS="tzdata build-essential python3-setuptools python3-pip apt-utils" \
	DEB_PACKAGES="locales libgdal20 python3-gdal python3-fiona python3-rasterio python3-pyproj ${ADD_DEB_PACKAGES}" \
	PIP_PACKAGES="jupyter wheel==0.33.4 ${ADD_PIP_PACKAGES}"

COPY ./requirements.txt /jupyter/requirements.txt

# Run all installs
RUN \
	# Install dependencies
	apt-get update \
	&& apt-get --no-install-recommends install -y ${DEB_BUILD_DEPS} ${DEB_PACKAGES} \
	# Timezone
	&& cp /usr/share/zoneinfo/${TZ} /etc/localtime\
	&& dpkg-reconfigure tzdata \
	# Locale
	&& sed -i -e "s/# ${LOCALE} UTF-8/${LOCALE} UTF-8/" /etc/locale.gen \
	&& dpkg-reconfigure --frontend=noninteractive locales \
	&& update-locale LANG=${LOCALE} \
	&& echo "For ${TZ} date=$(date)" && echo "Locale=$(locale)" \
	&& pip3 install ${PIP_PACKAGES} \
	&& pip3 install -r /jupyter/requirements.txt \
	&& apt-get remove --purge ${DEB_BUILD_DEPS} -y \
	&& apt autoremove -y  \
	&& rm -rf /var/lib/apt/lists/* 

COPY ./entrypoint.sh /jupyter/start.sh

WORKDIR /jupyter/content/notebooks
ENTRYPOINT ["/jupyter/start.sh"]

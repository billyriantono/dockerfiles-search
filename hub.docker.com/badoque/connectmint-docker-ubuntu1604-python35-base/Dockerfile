FROM ubuntu:16.04

RUN apt-get update && apt-get install -y \
	build-essential \
	libav-tools \
	python-dev \
	cython \
	libavcodec-dev \
	libavformat-dev \
	libswscale-dev \
	libpq-dev \
	libgdal-dev \
	wget \
	git \
	zlib1g-dev \
	libjpeg-turbo8-dev \
	liblcms2-dev 

# ensure local python is preferred over distribution python
ENV PATH /usr/local/bin:$PATH

# http://bugs.python.org/issue19846
# > At the moment, setting "LANG=C" on a Linux system *fundamentally breaks Python 3*, and that's not OK.
ENV LANG C.UTF-8

# runtime dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
		tcl \
		tk \
	&& rm -rf /var/lib/apt/lists/*

ENV GPG_KEY 97FC712E4C024BBEA48A61ED3A5CA953F73C700D
ENV PYTHON_VERSION 3.5.3

# if this is called "PIP_VERSION", pip explodes with "ValueError: invalid truth value '<VERSION>'"
ENV PYTHON_PIP_VERSION 9.0.1
ENV PYTHON_SETUPTOOLS_VERSION 35.0.1
ENV PYTHON_WHEEL_VERSION 0.29.0

RUN set -ex \
	&& buildDeps=' \
		tcl-dev \
		tk-dev \
	' \
	&& apt-get update && apt-get install -y $buildDeps --no-install-recommends && rm -rf /var/lib/apt/lists/* \
	\
	&& wget -O python.tar.xz "https://www.python.org/ftp/python/${PYTHON_VERSION%%[a-z]*}/Python-$PYTHON_VERSION.tar.xz" \
	&& wget -O python.tar.xz.asc "https://www.python.org/ftp/python/${PYTHON_VERSION%%[a-z]*}/Python-$PYTHON_VERSION.tar.xz.asc" \
	&& export GNUPGHOME="$(mktemp -d)" \
	&& gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$GPG_KEY" \
	&& gpg --batch --verify python.tar.xz.asc python.tar.xz \
	&& rm -r "$GNUPGHOME" python.tar.xz.asc \
	&& mkdir -p /usr/src/python \
	&& tar -xJC /usr/src/python --strip-components=1 -f python.tar.xz \
	&& rm python.tar.xz \
	\
	&& cd /usr/src/python \
	&& ./configure \
		--enable-loadable-sqlite-extensions \
		--enable-shared \
	&& make -j$(nproc) \
	&& make install \
	&& ldconfig \
	\
# explicit path to "pip3" to ensure distribution-provided "pip3" cannot interfere
	&& if [ ! -e /usr/local/bin/pip3 ]; then : \
		&& wget -O /tmp/get-pip.py 'https://bootstrap.pypa.io/get-pip.py' \
		&& python3 /tmp/get-pip.py "pip==$PYTHON_PIP_VERSION" \
		&& rm /tmp/get-pip.py \
	; fi \
# we use "--force-reinstall" for the case where the version of pip we're trying to install is the same as the version bundled with Python
# ("Requirement already up-to-date: pip==8.1.2 in /usr/local/lib/python3.6/site-packages")
# https://github.com/docker-library/python/pull/143#issuecomment-241032683
	&& pip3 install --no-cache-dir --upgrade --force-reinstall \
		"pip==$PYTHON_PIP_VERSION" \
		"setuptools==$PYTHON_SETUPTOOLS_VERSION" \
		"wheel==$PYTHON_WHEEL_VERSION" \
	\
	&& find /usr/local -depth \
		\( \
			\( -type d -a -name test -o -name tests \) \
			-o \
			\( -type f -a -name '*.pyc' -o -name '*.pyo' \) \
		\) -exec rm -rf '{}' + \
	&& apt-get purge -y --auto-remove $buildDeps \
	&& rm -rf /usr/src/python ~/.cache

# make some useful symlinks that are expected to exist
RUN cd /usr/local/bin \
	&& { [ -e easy_install ] || ln -s easy_install-* easy_install; } \
	&& ln -s idle3 idle \
	&& ln -s pydoc3 pydoc \
	&& ln -s python3 python \
	&& ln -s python3-config python-config

RUN pip install \
	adjacent==1.0.0 \
	awesome-slugify==1.6.5 \
	boto==2.42.0 \
	celery==3.1.23 \
	cent==2.0.2 \
	Collectfast==0.2.3 \
	django-allauth==0.27.0 \
	django-anymail==0.4.2 \
	django-autoslug==1.9.3 \
	django-boto==0.3.9 \
	django-braces==1.9.0 \
	django-compressor==2.1 \
	django-cors-middleware==1.3.1 \
	django-crispy-forms==1.6.0 \
	django-environ==0.4.0 \
	django-filter==0.14.0 \
	django-filters==0.2.1 \
	django-model-utils==2.5.2 \
	django-paypal==0.3.3 \
	django-push-notifications==1.4.1 \
	django-redis==4.4.4 \
	django-rest-auth==0.8.1 \
	django-storages-redux==1.3.2 \
	django==1.10.6 \
	djangorestframework-gis==0.10.1\
	djangorestframework-jwt==1.8.0 \
	djangorestframework==3.4.6 \
	drfdocs==0.0.11 \
	gevent==1.1.2 \
	git+https://github.com/badoque/django-bdq-s3-images.git \
	git+https://github.com/badoque/django-bdq-utils.git \
	git+https://github.com/badoque/fcm-django.git \
	git+https://github.com/badoque/PyFCM.git \
	git+https://github.com/radek-senfeld/ffvideo.git \
	gunicorn==19.6.0 \
	ipdb \
	markdown==2.6.6 \
	numpy==1.12.0 \
	opbeat==3.4.0 \
	Pillow==3.3.1 \
	psycopg2==2.6.2 \
	PyJWT==1.4.2 \
	pytz==2016.6.1 \
	raven==5.26.0 \
	rcssmin==1.0.6 \
	redis>=2.10.0 \
	wheel==0.29.0 


CMD ["python3"]

FROM python:3.5-alpine3.8

MAINTAINER Evgeniy Klemin "evgeniy.klemin@gmail.com"

ARG CONT_IMG_VER=alpine35-full-0.2.1
ENV CONT_IMG_VER $CONT_IMG_VER


#==========================================================
#                        PACKAGES
#==========================================================
RUN apk add -U --no-cache --virtual .build-deps \
        # common
        mariadb-dev \
        gcc \
        musl-dev \
        python-dev \
        # lxml
        libxslt-dev \
        libc-dev \
        # Pillow
        jpeg-dev \
        zlib-dev \
        freetype-dev \
        openjpeg-dev \
        file-dev \
        # pandas
        alpine-sdk \
        # scipy
        gfortran \
        build-base \
        libpng-dev \
        openblas-dev \
        # pybrain
        build-base \
        libffi-dev \
        libressl-dev \
    # numpy
    && ln -s /usr/include/locale.h /usr/include/xlocale.h \
	&& pip install mysqlclient==1.3.13 \
        # system
        lxml \
        # edxsession
        virtualenv \
        # pillow
        python-magic \
        Pillow==5.2.* \
        # numpy,scipy,pandas
        python-dateutil \
        numpy==1.14.3 \
        scipy==0.19.* \
        pandas==0.23.0 \
        # pybrain
        structure \
        git+https://github.com/pybrain/pybrain.git \
    && find /usr/local -depth \
		\( \
			\( -type d -a \( -name test -o -name tests \) \) \
			-o \
			\( -type f -a \( -name '*.pyc' -o -name '*.pyo' \) \) \
		\) -exec rm -rf '{}' + \
    && apk add --no-cache --virtual .runtime-deps \
        mariadb-connector-c \
        musl \
        # edxsession
        python2 \
        # django tests
        sqlite \
        # pip
        git \
        # Pillow
        libmagic \
        jpeg \
        freetype \
        openjpeg \
        # scipy
        libgfortran \
        libgcc \
        libpng \
        libstdc++ \
        openblas \
        # pybrain
        libffi \
	&& apk del .build-deps \
    && rm -rf /usr/local/lib/python3.5/site-packages/magic/


#==========================================================
#                      WORKDIR
#==========================================================
WORKDIR /app


#==========================================================
#                        CONFIGS
#==========================================================
EXPOSE 8000


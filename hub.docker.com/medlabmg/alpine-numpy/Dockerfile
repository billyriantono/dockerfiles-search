FROM python:3.7-alpine3.9

RUN apk --no-cache add gcc gfortran python3-dev build-base libstdc++ wget freetype-dev libpng-dev openblas-dev \
	&& ln -s /usr/include/locale.h /usr/include/xlocale.h \
	&& pip3 install numpy \
	&& pip3 install --no-cache-dir scipy pandas matplotlib

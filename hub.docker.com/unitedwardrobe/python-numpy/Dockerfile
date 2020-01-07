FROM publysher/alpine-numpy:1.14.0-python3.6-alpine3.7

RUN apk add --no-cache build-base libpng-dev openblas-dev freetype-dev
RUN ln -s /usr/include/locale.h /usr/include/xlocale.h

COPY requirements.txt /tmp/requirements.txt

RUN pip install --upgrade pip
RUN pip install --no-cache-dir -r /tmp/requirements.txt
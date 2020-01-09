FROM ubuntu:bionic
MAINTAINER Carlo de Franchis <carlodef@gmail.com>
RUN apt update && apt install -y \
    build-essential \
    libhdf5-dev \
    libhdf4-alt-dev \
    libhdf4-0-alt \
    libnetcdf-dev \
    libcurl4-gnutls-dev \
    libopenjp2-7-dev \
    libzstd-dev \
    libssl-dev \
    liblzma-dev \
    file \
    python3 \
    python3-dev \
    curl \
    vim
RUN curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
RUN python3 get-pip.py
RUN pip install ipython

WORKDIR /usr/src/app/gdal
RUN apt-get install -y wget unzip
RUN wget https://github.com/OSGeo/gdal/archive/dd4de9ef0f2444d33437e0cbd09e94270da790ac.zip
RUN unzip dd4de9ef0f2444d33437e0cbd09e94270da790ac.zip && \
    cd gdal-dd4de9ef0f2444d33437e0cbd09e94270da790ac/gdal/ && \
    ./configure --with-geotiff=internal --with-libtiff=internal && \
    make -j 32 install

RUN pip install -I numpy boto3 && \
    pip install rasterio \
      --global-option build_ext \
      --global-option=`gdal-config \
      --cflags` --global-option build_ext \
      --global-option=-L`gdal-config \
      --prefix`/unix/lib/

# Rasterio curl certificate compatibility on ubuntu
# See section 'Configuration' of https://github.com/mapbox/rasterio/issues/942
ENV CURL_CA_BUNDLE /etc/ssl/certs/ca-certificates.crt

ENV TERM xterm-color
ENTRYPOINT ["bash"]

ENV LD_LIBRARY_PATH /usr/local/lib:$LD_LIBRARY_PATH

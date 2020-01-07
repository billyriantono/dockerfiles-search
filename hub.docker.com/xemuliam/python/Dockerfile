FROM       alpine
MAINTAINER Viacheslav Kalashnikov <xemuliam@gmail.com>
RUN        apk add --no-cache \
               bash \
               ca-certificates \
               build-base \
               gfortran \
               python3 \
               python3-dev \
               python3-tkinter \
               freetype-dev \
               libpng-dev \
               jpeg-dev \
               lapack-dev \
               libxml2-dev \
               libxslt-dev \
           && pip3.6 install --upgrade pip \
           && pip3.6 install \
                  py4j \
                  numpy \
                  scipy \
                  pandas \
                  matplotlib
RUN        echo "manylinux1_compatible = True" > /usr/lib/python3.6/_manylinux.py \
           && cd /usr/bin \
           && ln -sf easy_install-3.6 easy_install \
           && ln -sf idle3.6 idle \
           && ln -sf pydoc3.6 pydoc \
           && ln -sf python3.6 python \
           && ln -sf python-config3.6 python-config \
           && ln -sf pip3.6 pip \
           && ln -sf /usr/include/locale.h /usr/include/xlocale.h
CMD python

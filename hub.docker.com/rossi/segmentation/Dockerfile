FROM tensorflow/tensorflow:latest-jupyter

RUN apt-get update \
  && apt-get install -y --no-install-recommends python-pip python-dev vim libsm6 libxext6 libgtk2.0-dev curl libtiff5-dev \
  && pip install --upgrade scikit-image keras opencv-python PyDrive \
  && rm -rf /var/lib/apt/lists/*

RUN curl -sfLO http://www.imagemagick.org/download/ImageMagick-7.0.8-25.tar.gz \
  && tar -xzf ImageMagick-7.0.8-25.tar.gz \
  && cd ImageMagick-7.0.8-25 \
  && ./configure --with-libtiff --prefix /usr/local \
  && make install \
  && cd .. \
  && rm -rf  ImageMagick* \
  && ldconfig /user/local/lib

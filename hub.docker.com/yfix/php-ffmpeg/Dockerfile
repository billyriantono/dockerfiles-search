FROM yfix/php

RUN echo "deb http://ppa.launchpad.net/mc3man/trusty-media/ubuntu trusty main" > /etc/apt/sources.list.d/mc3man-trusty-media-trusty.list \
  && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys ED8E640A \
  \
  && apt-get update \
  \
  && apt-cache search ffmpeg 2>&1 \
  \
  && apt-get install -y \
    ffmpeg \
    gstreamer0.10-ffmpeg \
  \
  && echo "=========" \
  \
  && apt-get autoremove -y \
  && apt-get clean -y \
  && rm -rf /var/lib/apt/lists/*

COPY docker /

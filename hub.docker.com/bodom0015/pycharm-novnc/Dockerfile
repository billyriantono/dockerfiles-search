FROM bodom0015/novnc-base:fix-pycharm-2017

RUN apt-get -qq update && \
    apt-get -qq install --no-install-recommends \
      python-pip \
      python-dev \
      build-essential && \
    pip install --upgrade pip && \
    apt-get -qq clean all && \
    apt-get -qq autoclean && \
    apt-get -qq autoremove && \
    rm -rf /var/lib/apt/lists/* /tmp/*

RUN cd / && \
   wget -q http://download.jetbrains.com/python/pycharm-community-2017.2.tar.gz && \
   tar xvfz pycharm-community-2017.2.tar.gz &&  \
   rm pycharm-community-2017.2.tar.gz

ADD init.sh /init.sh

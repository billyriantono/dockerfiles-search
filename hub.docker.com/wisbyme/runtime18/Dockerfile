FROM wisbyme/ubuntu18

LABEL maintainer="ljjun<wisbyme@gmail.com>"

ENV PATH /opt/conda/bin:$PATH

ENV P_VER  4.7.10
ENV Q_VER  5.9.8
ENV PyVER  3

COPY setupenv.sh /tmp/setupenv.sh

RUN apt-get update -y --fix-missing \
 && apt-get install -y --no-install-recommends \
    wget bzip2 gzip \
 && wget --tries=0 --quiet https://repo.anaconda.com/miniconda/Miniconda${PyVER}-${P_VER}-Linux-x86_64.sh -O /tmp/anaconda.sh \
 && /bin/bash /tmp/anaconda.sh -b -p /opt/conda \
 && rm /tmp/anaconda.sh \
 && ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh \
 && echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc \
 && echo "conda activate base" >> ~/.bashrc \
 && /opt/conda/bin/conda clean -tipsy \
 && mkdir -p /usr/lib/qt5 \
 && wget --tries=0 --quiet https://raw.githubusercontent.com/programs/qtdist/master/qt${Q_VER}_linux64.tar.gz -O /tmp/qt5dist.tar.gz \
 && tar -C /usr/lib/qt5 -zxvf /tmp/qt5dist.tar.gz \
 && touch /etc/ld.so.conf.d/qt5.conf \
 && echo "/usr/lib/qt5" >> /etc/ld.so.conf.d/qt5.conf \
 && /sbin/ldconfig \
 && echo "export QTDIR=/usr/lib/qt5" >> ~/.bashrc \
 && echo "export PATH=$PATH:/usr/lib/qt5" >> ~/.bashrc \
 && chmod +x /tmp/setupenv.sh \
 && /tmp/setupenv.sh \
 && apt-get autoremove -y \
 && apt-get autoclean -y \
 && rm -rf /var/cache/apt/* /var/lib/apt/lists/* /tmp/* /var/tmp/* \
 && /sbin/install_clean

WORKDIR /home

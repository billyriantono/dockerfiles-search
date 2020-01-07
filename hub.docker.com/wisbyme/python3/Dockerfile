FROM wisbyme/ubuntu16

LABEL maintainer="ljjun<wisbyme@gmail.com>"

ENV PATH /opt/conda/bin:$PATH
ENV P_VER  4.7.10
ENV PyVER  3
COPY setupenv.sh /tmp/setupenv.sh

RUN apt-get update -y --fix-missing \
 && apt-get install -y --no-install-recommends wget bzip2 gzip \
 && wget --no-check-certificate --tries=0 --quiet https://repo.anaconda.com/miniconda/Miniconda${PyVER}-${P_VER}-Linux-x86_64.sh -O /tmp/anaconda.sh \
 && /bin/bash /tmp/anaconda.sh -b -p /opt/conda \
 && rm /tmp/anaconda.sh \
 && ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh \
 && echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc \
 && echo "conda activate base" >> ~/.bashrc \
 && /opt/conda/bin/conda clean -tipsy \
 && chmod +x /tmp/setupenv.sh \
 && /tmp/setupenv.sh \
 && apt-get autoremove -y \
 && apt-get autoclean -y \
 && rm -rf /var/cache/apt/* /var/lib/apt/lists/* /tmp/* /var/tmp/* \
 && /sbin/install_clean

WORKDIR /home

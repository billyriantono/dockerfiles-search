FROM ubuntu:16.04

ENV TZ="Europe/Helsinki"

RUN rm /bin/sh && ln -s /bin/bash /bin/sh

RUN \
  apt-get update && \
  apt-get -y dist-upgrade && \
  apt-get install -y build-essential openssh-client libsasl2-dev libldap2-dev libssl-dev libcurl4-openssl-dev jq git wget curl hunspell zlib1g-dev libbz2-dev liblzma-dev libncurses5-dev dh-autoreconf pkg-config autoconf && \
  apt-get install -y python2.7 python2.7-dev python-virtualenv python-pip python-pip-whl python-six && \
  apt-get install -y python3.5 python3.5-dev python3.5-venv python3-tk python3-six && \
  apt-get install -y gettext zlib1g-dev libtiff5-dev libjpeg8-dev libfreetype6-dev liblcms2-dev libwebp-dev graphviz-dev && \
  apt-get clean && \
  ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && \
  echo $TZ > /etc/timezone && \
  dpkg-reconfigure -f noninteractive tzdata

RUN \
  mkdir data && \
  pushd data && \
  mkdir unzip && \
  wget https://github.com/samtools/samtools/releases/download/1.4/samtools-1.4.tar.bz2 && \
  wget https://github.com/samtools/bcftools/releases/download/1.4/bcftools-1.4.tar.bz2 && \
  wget https://github.com/samtools/htslib/releases/download/1.4/htslib-1.4.tar.bz2 && \
  wget https://github.com/arq5x/bedtools2/releases/download/v2.26.0/bedtools-2.26.0.tar.gz && \
  wget https://github.com/bedops/bedops/releases/download/v2.4.26/bedops_linux_x86_64-v2.4.26.tar.bz2 && \
  wget https://github.com/vcftools/vcftools/tarball/master && \
  tar -xvjf htslib* -C unzip/ && \
  tar -xvjf bcftools* -C unzip/ && \
  tar -xvjf samtools* -C unzip/ && \
  tar -xvf bedtools* -C unzip/ && \
  tar -xvjf bedops* -C unzip/ && \
  tar -xvf master* -C unzip/ && \
  pushd unzip && \
  pushd htslib* && make && make install && popd && \
  pushd bcftools* && make && make install && popd && \
  pushd samtools* && make && make install && popd && \
  pushd bedtools* && make && make install && popd && \
  cp bin/* /usr/local/bin && \
  pushd vcftools* && ./autogen.sh && ./configure && make && make install && popd && \
  popd && \
  popd && \
  rm -rf data/

CMD ["bash"]

FROM debian:stretch-backports

MAINTAINER Patrick.Lezy <patrick.lezy@gmail.com>

# get patacrep packages dependencies

RUN 	apt-get update \
	&& DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y \
	python3 \
  python3-pip \
  texlive \
  texlive-latex-base \
  texlive-latex-recommended \
  texlive-latex-extra \
  texlive-lang-english \
  texlive-lang-french \
  texlive-lang-portuguese \
  texlive-lang-spanish \
  texlive-lang-italian \
  texlive-fonts-extra \
  texlive-luatex \
  texlive-xetex \
  lmodern \
  lilypond \
  curl \
  wget \
  git \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# setup python for patacrep
# for more informations about update-alternatives,
# see https://linuxconfig.org/how-to-change-default-python-version-on-debian-9-stretch-linux

RUN   update-alternatives --install /usr/bin/python python /usr/bin/python2.7 1 \
  &&  update-alternatives --install /usr/bin/python python /usr/bin/python3.5 2 \
  &&  curl -O https://bootstrap.pypa.io/get-pip.py \
  &&  python get-pip.py

# setup patacrep (development)

RUN   mkdir -p /patacrep \
  &&  cd /patacrep \
  &&  git clone git://github.com/patacrep/patacrep.git \
  &&  cd patacrep \
  &&  pip3 install -r Requirements.txt \
  &&  python3 setup.py develop

RUN   mkdir -p /data

VOLUME ["/data"]

COPY scripts /patacrep/scripts/

CMD /patacrep/scripts/update.sh




FROM mono:4.6.2.7

MAINTAINER "Aaron Walker" <a.walker@base2services.com>

RUN apt-get update && apt-get install -y \
	  python-pip \
          --no-install-recommends \
	&& rm -rf /var/lib/apt/lists/* \
  && pip install awscli \
  && mkdir -p /usr/src/app/source /usr/src/app/build

WORKDIR /usr/src/app/source

ONBUILD COPY . /usr/src/app/source
ONBUILD RUN nuget restore -NonInteractive
ONBUILD RUN xbuild /property:Configuration=Release /property:OutDir=/usr/src/app/build/

ONBUILD WORKDIR /usr/src/app/build

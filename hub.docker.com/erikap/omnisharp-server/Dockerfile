FROM mono:3.10

MAINTAINER Erika Pauwels <erika.pauwels@gmail.com>

ENV LOG_LEVEL Debug

RUN apt-get -y update; apt-get -y install git
RUN git clone https://github.com/erikap/omnisharp-server.git \
      && cd omnisharp-server \
      && git submodule update --init --recursive \
      && xbuild

EXPOSE 2000
WORKDIR /app

CMD mono /omnisharp-server/OmniSharp/bin/Debug/OmniSharp.exe -s /app -v ${LOG_LEVEL}

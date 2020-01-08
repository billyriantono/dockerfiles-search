FROM qnib/d-consul

RUN apt-get update \
 && apt-get install -y apt-transport-https lsb-release
ADD etc/apt/sources.list.d/nodesource.list /etc/apt/sources.list.d/
RUN curl -s https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add - \
 && apt-get update \
 && apt-get install -y nodejs

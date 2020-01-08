FROM wlanslovenija/runit

MAINTAINER Jernej Kos <jernej@kos.mx>

EXPOSE 27017/tcp

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-key 505A7412 && \
 echo "deb [arch=amd64] http://s3.amazonaws.com/tokumx-debs $(lsb_release -cs) main" > /etc/apt/sources.list.d/tokumx.list && \
 apt-get update -q -q && \
 apt-get --no-install-recommends --yes --force-yes install tokumx
 
COPY ./etc /etc


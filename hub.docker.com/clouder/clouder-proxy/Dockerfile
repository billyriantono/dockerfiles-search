FROM clouder/clouder-nginx
MAINTAINER Yannick Buron yburon@goclouder.net

RUN apt-get -qq update && DEBIAN_FRONTEND=noninteractive apt-get -y -qq install git bc
RUN git clone https://github.com/letsencrypt/letsencrypt /opt/letsencrypt
RUN /opt/letsencrypt/letsencrypt-auto certonly --help --agree-tos

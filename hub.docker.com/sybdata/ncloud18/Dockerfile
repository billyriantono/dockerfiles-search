FROM nginx:1.15.2

ENV DEBIAN_FRONTEND=noninteractive
WORKDIR /tmp

# set ports
EXPOSE 80 443

RUN \
apt-get update && apt-get upgrade -V && apt-get dist-upgrade && apt-get autoremove && \
apt-get install -y \
software-properties-common dirmngr \
wget \
mc \
nano \
tzdata \
htop && \
apt-key adv --recv-keys --keyserver keyserver.ubuntu.com 0xF1656F24C74CD1D8 && \
add-apt-repository 'deb [arch=amd64,i386,ppc64el] http://ftp.hosteurope.de/mirror/mariadb.org/repo/10.3/debian stretch main' && \
apt-get update && \
apt-get install certbot -y 

WORKDIR /
CMD ["/bin/bash"]

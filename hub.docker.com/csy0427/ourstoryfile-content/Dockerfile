FROM phusion/baseimage:0.11

LABEL maintainer="csek06"

VOLUME ["/opt/appdynamics"]

RUN export DEBIAN_FRONTEND=noninteractive && \
apt-get update && \
apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xF1656F24C74CD1D8 && \
add-apt-repository "deb [arch=amd64,arm64,ppc64el] http://mariadb.mirror.liquidtelecom.com/repo/10.4/ubuntu $(lsb_release -cs) main" && \
curl -sL https://deb.nodesource.com/setup_13.x | bash - && \
apt-get install -y \
iputils-ping mariadb-client mariadb-server nano nginx nodejs tzdata unzip wget && \
usermod -u 99 nobody && \
usermod -g 100 nobody && \
mkdir -p /etc/my_init.d && \
mkdir -p /agent-maintainer/builder && \
mkdir -p /agent-maintainer/nginx

COPY firstrun.sh /etc/my_init.d/firstrun.sh
COPY scripts/safe-shutdown.sh /etc/my_init.pre_shutdown.d/safe-shutdown.sh
COPY react/ /agent-maintainer/builder/
COPY nginx/ /agent-maintainer/nginx/
RUN chmod +x /etc/my_init.d/firstrun.sh && \
chmod +x /etc/my_init.pre_shutdown.d/safe-shutdown.sh

FROM phusion/baseimage:0.9.16
MAINTAINER sparklyballs <sparkly@madeupemail.com>

# Set correct environment variables
ENV DEBIAN_FRONTEND=noninteractive HOME="/root" TERM=xterm

# set ports
EXPOSE 55413 55414 55415 35623

# Use baseimage-docker's init system
CMD ["/sbin/my_init"]

# Add required files that are local
ADD src/ /root/

# Fix a Debianism of the nobody's uid being 65534
RUN usermod -u 99 nobody && \
usermod -g 100 nobody && \

# fix startup file
chmod +x /root/startup-files/start.sh && \

# add repo, update apt and install build dependencies
add-apt-repository ppa:uroni/urbackup && \
apt-get update -q && \
apt-get -y install urbackup-server && \

# clean up
apt-get clean -y && \
rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
/usr/share/man /usr/share/groff /usr/share/info \
/usr/share/lintian /usr/share/linda /var/cache/man && \
(( find /usr/share/doc -depth -type f ! -name copyright|xargs rm || true )) && \
(( find /usr/share/doc -empty|xargs rmdir || true )) && \

mkdir -p /var/urbackup && \
ln -s /var/urbackup /config

CMD ["/root/startup-files/start.sh"]


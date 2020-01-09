FROM djmattyg007/arch-runit-base:2017.10.27-1
MAINTAINER djmattyg007

ENV GRAFANAIMAGE_VERSION=2017.10.27-2

# Add install bash script
COPY setup/root/*.sh /root/
COPY setup/init.sh /etc/service/grafana/run

# Run bash script to install php-fpm
RUN /root/install.sh && \
    rm /root/install.sh /root/grafana.sh

ENTRYPOINT ["/usr/bin/init"]

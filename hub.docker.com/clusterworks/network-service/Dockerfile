FROM centos:7

RUN yum -y install dnsmasq git make wget

# install n
WORKDIR /
RUN git clone https://github.com/tj/n.git \
    && cd n \
    && make \
    && make install \
    && cd .. \
    && rm -r n

# use n to install node
RUN n lts

# use npm to install config-templater
RUN npm install -g config-templater

# copy template files
RUN mkdir -p /etc/config-templates/dnsmasq
ADD dnsmasqconf.template /etc/config-templates/dnsmasq/dnsmasqconf.template
ADD hosts.template /etc/config-templates/dnsmasq/hosts.template
ADD template-config.yml /etc/config-templates/dnsmasq/template-config.yml

# pull the ipxe rom with proxy support
RUN mkdir -p /var/lib/tftpboot \
    && cd /var/lib/tftpboot \
    && wget https://github.com/clusterworks/ipxe/releases/download/160817/undionly.kpxe

# add default ipxe script
ADD default.ipxe /var/lib/tftpboot/default.ipxe

# add the entry point
COPY entrypoint.sh /entrypoint.sh

EXPOSE 53/udp
EXPOSE 53/tcp
EXPOSE 67/udp
EXPOSE 68/udp
EXPOSE 69/udp

ENTRYPOINT ["/entrypoint.sh"]

CMD ["dnsmasq", "--no-daemon"]

FROM fedora:26
MAINTAINER Christopher Williams

#
# Add openvpn init script
# 
ADD openvpn.sh /openvpn.sh
RUN chmod 755 /openvpn.sh

#
# Install openvpn
#

RUN dnf -y install openvpn \
    && dnf clean all \
    && rm -rf /var/cache/yum


#
# Define containter settings
#

VOLUME ["/openvpn_conf"]

WORKDIR /openvpn_conf

ENTRYPOINT ["/openvpn.sh"]
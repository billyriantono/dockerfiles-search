#FROM titpetric/netdata
FROM firehol/netdata
MAINTAINER Tikia "renaud@tikia.net"

#Config netdata
RUN echo "[global]" >> /etc/netdata/netdata.conf
RUN echo "      history = 86400" >> /etc/netdata/netdata.conf
RUN echo "      hostname = sd-116866" >> /etc/netdata/netdata.conf

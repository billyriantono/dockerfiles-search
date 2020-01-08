#FROM ubuntu:14.04

FROM joaniznardo/ubuntum7baseb

MAINTAINER joaniznardo (github)

ENV DEBIAN_FRONTEND=noninteractive
#RUN apt-get update && apt-get install -y openssh-server sudo supervisor
#RUN useradd -m ubuntu && echo "ubuntu:ubuntu" | chpasswd && adduser ubuntu sudoRUN echo "# Interfaces the DHCP relay should listen on:" | debconf-set-selections && echo "isc-dhcp-relay	isc-dhcp-relay/interfaces	string	" | debconf-set-selections && echo "# Servers the DHCP relay should forward requests to:" | debconf-set-selections && echo "isc-dhcp-relay	isc-dhcp-relay/servers	string" | debconf-set-selections && echo "# Additional options for the DHCP relay daemon:" | debconf-set-selections && echo "isc-dhcp-relay	isc-dhcp-relay/options	string	" | debconf-set-selections

RUN apt-get install -q -y -o "DPkg::Options::=--force-confold" -o "DPkg::Options::=--force-confdef" isc-dhcp-relay 

#CMD /etc/init.d/ssh restart && supervisord -n

FROM ubuntu:16.04

RUN apt-get update && apt-get upgrade -y && apt-get install bind9 -y && apt-get install nano -y

ADD https://raw.githubusercontent.com/VareTom/WoodyToys-WT4-/master/DockerDNS/confDNS/named.conf /etc/bind/
ADD https://raw.githubusercontent.com/VareTom/WoodyToys-WT4-/master/DockerDNS/confDNS/named.conf.options /etc/bind/
ADD https://raw.githubusercontent.com/VareTom/WoodyToys-WT4-/master/DockerDNS/confDNS/named.conf.local /etc/bind/
ADD https://raw.githubusercontent.com/VareTom/WoodyToys-WT4-/master/DockerDNS/confDNS/named.conf.default-zones /etc/bind/
ADD https://raw.githubusercontent.com/VareTom/WoodyToys-WT4-/master/DockerDNS/confDNS/db.wt4.ephec-ti.be /etc/bind/
ADD https://raw.githubusercontent.com/VareTom/WoodyToys-WT4-/master/DockerDNS/confDNS/db.local.wt4.ephec-ti.be /etc/bind/

EXPOSE 53/tcp 53/udp

CMD ["/usr/sbin/named", "-g", "-c", "/etc/bind/named.conf", "-u", "bind"]

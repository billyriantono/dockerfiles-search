FROM 			debian:stretch
MAINTAINER		<cnaranjo@nsoporte.com>


COPY			files/ns-start /usr/bin/



RUN				apt-get update; apt-get -y upgrade; \
				apt-get -y install openvpn easy-rsa; \
				make-cadir /etc/openvpn/ca; \
				ln -s /etc/openvpn/ca/openssl-1.0.0.cnf /etc/openvpn/ca/openssl.cnf; \
				tar -czvf /opt/data.tgz /etc/openvpn; \
				rm -rf /etc/openvpn; \
				mkdir -p /etc/openvpn; \
				chmod +x /usr/bin/ns-start



ENTRYPOINT		[ "/usr/bin/ns-start" ]



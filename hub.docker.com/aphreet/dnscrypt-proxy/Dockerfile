FROM ubuntu:17.04

RUN apt-get update \ 
	&& apt-get install -y dnscrypt-proxy wget \
	&& wget https://raw.githubusercontent.com/jedisct1/dnscrypt-proxy/master/dnscrypt-resolvers.csv -O /var/dnscrypt-resolvers.csv

EXPOSE 53

ENTRYPOINT ["/usr/sbin/dnscrypt-proxy"]

CMD ["-L", "/var/dnscrypt-resolvers.csv", "-a", "0.0.0.0", "-R", "ns0.dnscrypt.is"]

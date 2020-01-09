FROM uberchuckie/observium:1.4
MAINTAINER Jessica Smith <jess@mintopia.net>
RUN \
	apt-get -y update && \
	apt-get -y install php-ldap && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/*
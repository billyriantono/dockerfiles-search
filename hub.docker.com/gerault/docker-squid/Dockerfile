# from debian stretch backports
FROM gerault/docker-debian-stretch-backports
MAINTAINER Mathieu Gerault <mathieu.gerault@gamil.com>
LABEL Description="Squid server from Mathieu GERAULT"

# install squid
RUN apt-get update \
	&& apt-get install -y squid \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/*

# squid port
EXPOSE 3128

# entrypoint
COPY entrypoint.sh /entrypoint.sh
RUN chmod 755 /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]

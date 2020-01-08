# Couchbase Server for Ubuntu 14.04
#
# GitHub - http://github.com/dalekurt/docker-couchbase-server
# Docker Hub - http://hub.docker.com/u/dalekurt/couchbase-server
# Twitter - http://www.twitter.com/dalekurt

FROM aviata/ubuntu
MAINTAINER jmarsh.ext@aviatainc.com "jmarsh.ext@aviatainc.com"

ENV CB_USERNAME		Administrator
ENV CB_PASSWORD		couchbaseadmin
ENV CB_REST_USERNAME	Administrator
ENV CB_REST_PASSWORD	couchbaseadmin
ENV CB_BUCKET		mystuff

# Basic environment setup
# note: SpiderMonkey build req's: https://developer.mozilla.org/en-US/docs/Mozilla/Developer_guide/Build_Instructions/Linux_Prerequisites
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update \
	&& apt-get install -y librtmp0 python-httplib2 language-pack-en-base  \
	&& dpkg-reconfigure locales

# Downloading and Installing Couchbase
ENV CB_VERSION 3.0.3
# The file name has changed for previous version 2.x.x
# ENV CB_FILENAME couchbase-server-enterprise_${CB_VERSION}_x86_64.deb
#
ENV CB_FILENAME couchbase-server-enterprise_${CB_VERSION}-ubuntu12.04_amd64.deb
ENV CB_SOURCE http://packages.couchbase.com/releases/$CB_VERSION/$CB_FILENAME

RUN wget -O/tmp/$CB_FILENAME $CB_SOURCE && \
	dpkg -i /tmp/$CB_FILENAME && \
	rm /tmp/$CB_FILENAME

# SpiderMonkey, jsawk, and resty - these are used for the docker-couchbase script.
# The echo prints out the current buckets for tracing in the log file.
RUN apt-get install -y libmozjs-24-bin \
	&& ln -s /usr/bin/js24 /usr/local/bin/js \
	&& echo "export JS=/usr/local/bin/js" > /etc/jsawkrc \
	&& wget -O/usr/local/bin/jsawk http://github.com/micha/jsawk/raw/master/jsawk \
	&& wget -O/usr/local/bin/resty http://github.com/micha/resty/raw/master/resty \
	&& chmod +x /usr/local/bin/jsawk /usr/local/bin/resty \
	&& { \
		echo ""; \
		echo "source /usr/local/bin/resty -W 'http://localhost:8091/pools/default'"; \
		echo ""; \
	} >> /etc/bash.bashrc

# Create directory structure for volume sharing
RUN mkdir -p /app \
	&& mkdir -p /app/data \
	&& mkdir -p /app/index \
	&& mkdir -p /app/resources \
	&& mkdir -p /app/conf \
	&& mkdir -p /app/backup \
	&& mkdir -p /app/logs \
	&& chown -R couchbase:couchbase /app
VOLUME ["/app/data"]
VOLUME ["/app/backup"]
VOLUME ["/app/logs"]

# Add bootstrapper.  Copy the script into the docker container.
ADD resources/docker-couchbase /usr/local/bin/docker-couchbase
# Export couchbase path so the commands are accessible from the command line.
RUN export PATH=$PATH:/opt/couchbase/bin \
	&& echo "export PATH=$PATH:/opt/couchbase/bin" >> /etc/bash.bashrc
# These ports are exposed even outside of a docker-compose launch.
EXPOSE 4369 8091 8092 11209 11210 11211 11214 11215 18091 18092 21100-21299

# Add backup to /app/backup.  Copy in the backup files.
# Conider: we may want to do a volume mount here if we don't want to put out database image under source control.
# ADD backup /app/backup

# Add Resources
ADD resources/couchbase.txt /app/resources/couchbase.txt
# ADD resources/docker.txt /app/resources/docker.txt
# This files containts the list of buckets to create:
ADD resources/default.conf /app/conf/default.conf

ENTRYPOINT ["docker-couchbase"]
CMD	["initial"]

FROM ubuntu
MAINTAINER Athurg Gooth<athurg@gooth.org>

RUN apt-get update && apt-get install -y \
		python2.7 \
		memcached \
		libmemcached-dev \
		python-setuptools \
		python-imaging \
		python-ldap \
		python-mysqldb \
		python-memcache \
		python-pylibmc \
		python-pip \
		python-urllib3 \
	&& pip install --no-cache-dir django-pylibmc \
	&& apt-get autoremove -y python-pip \
	&& rm -rf /var/lib/apt/lists/*
ADD wrapper.sh /

WORKDIR /haiwen
VOLUME /haiwen
EXPOSE 8000 8082
CMD /wrapper.sh

From alpine
MAINTAINER Arvind Rawat <arvind.rawat@amdocs.com>

RUN apk add --update --no-cache bash \
 				curl \
				python \
   			        python-dev \
       			        py-pip \
   			        build-base \
				libffi-dev \
			        openssl-dev \
				python3 \
				python3-dev \ 
				linux-headers \
			       && pip install virtualenv \
			       && pip install python-openstackclient \
			       && pip install python-novaclient \
			       && rm -rf /var/cache/apk/*


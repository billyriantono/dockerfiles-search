FROM ubuntu
RUN 	apt-get update &&\
	apt-get install -y \
		build-essential \
		libpython-dev \
		python-setuptools \
		python-openssl	\
		libffi-dev \
		libssl-dev \
		ssh \
		wget \
		curl \
		vim
RUN	easy_install pip
RUN	pip install pyopenssl ndg-httpsclient pyasn1
RUN	pip install python-openstackclient

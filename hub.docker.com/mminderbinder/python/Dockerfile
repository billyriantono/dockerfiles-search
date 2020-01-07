# mminderbinder/python
# Docker image with Python (2 & 3), pip, virutalenv, and virtualenvwrapper
FROM mminderbinder/baseimage
MAINTAINER Milo Minderbinder <minderbinder.enterprises@gmail.com>

# Install python & lmxl dependencies
RUN apt-get update && apt-get -y install \
	python \
	python3 \
	python-dev \
	python3-dev \
	libxml2-dev \
	libxslt-dev \
	lib32z1-dev

WORKDIR /root
ADD https://bootstrap.pypa.io/get-pip.py get-pip.py
RUN python get-pip.py
COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt

ENV PYTHON_PROJECTS_DIR=/mnt/python-projects \
	PROJECT_HOME=/mnt/python-projects \
	WORKON_HOME=/mnt/python-projects/.virtualenvs

VOLUME $PYTHON_PROJECTS_DIR
VOLUME $WORKON_HOME

COPY virtualenv-setup.sh virtualenv-setup.sh
RUN chmod 550 virtualenv-setup.sh
RUN ["/bin/bash", "-c", "/root/virtualenv-setup.sh"]

# Clean up APT when done
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
CMD ["/sbin/my_init"]

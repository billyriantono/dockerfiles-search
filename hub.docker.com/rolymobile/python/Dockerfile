FROM rolymobile/ubuntu:14.04

ENV PYTHON_VERSION 2.7.9

# Install Python compile needs
RUN apt-get update -qqy && \
	apt-get purge -y python.* && \
	apt-get install --no-install-recommends -qqy  build-essential sqlite3 libsqlite3-tcl libsqlite3-dev python-bsddb3 python-tk libgdbm-dev libreadline-dev libncurses5-dev libbz2-dev \
	wget \
	python-dev \
	python-pip \
	python-setuptools \
	libcurl4-openssl-dev && \
	rm -rf /var/lib/apt/lists/* && \
	pip install -U pip

# Download Python source code and compile
WORKDIR /tmp
RUN wget https://www.python.org/ftp/python/$PYTHON_VERSION/Python-$PYTHON_VERSION.tgz && \
	tar zxvf Python-$PYTHON_VERSION.tgz && \
	cd Python-$PYTHON_VERSION && \
	./configure --enable-unicode=ucs4 && \
	make && \
	make install && \
	cd ../ && \
	rm Python-$PYTHON_VERSION.tgz && \
	rm -rf Python-$PYTHON_VERSION && \
	pip install pycurl

# set Python  environment variables
RUN echo "\nexport PYTHONPATH=$PYTHONPATH:/usr/local/lib/python2.7/dist-packages/" >> ~/.bashrc

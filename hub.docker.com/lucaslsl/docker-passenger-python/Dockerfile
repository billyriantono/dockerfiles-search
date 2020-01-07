FROM phusion/passenger-customizable:0.9.17

RUN apt-get update && apt-get install -y \
	python \
	python-pip \
	python-dev \
	libjpeg-dev \
	libpq-dev \
	nodejs

RUN ln -sf /usr/bin/nodejs /usr/bin/node	


# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
FROM ubuntu:bionic

# Install required python & git packages
RUN apt-get update && apt-get install -y\
	python3.6-dev \
	python3-pip \
	openssl \
	nagios-nrpe-server

# Install python modules
RUN pip3 install paramiko paramiko-expect

# Clean cashe
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Add script that starts the NRPE server
ADD start.sh /start.sh

# Start NRPE server
CMD /start.sh
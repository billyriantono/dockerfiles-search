# Deployment path:  $DOCKER_FILE_PATH/blj_basic_py2.Dockerfile

ARG DOCKER_HUB_USER=biolockj
FROM $DOCKER_HUB_USER/blj_basic
ARG DEBIAN_FRONTEND=noninteractive

#1.) Install Ubuntu Software 
RUN apt-get install -y \
		python2.7-dev \
		python-pip \
		python-tk 
	
#2.) Cleanup
RUN	rm -rf /tmp/* && \
	rm -rf /var/log/* 

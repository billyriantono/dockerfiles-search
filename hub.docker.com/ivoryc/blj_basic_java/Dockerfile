# Deployment path:  $DOCKER_FILE_PATH/blj_basic_java.Dockerfile

ARG DOCKER_HUB_USER=biolockj
FROM $DOCKER_HUB_USER/blj_basic
ARG DEBIAN_FRONTEND=noninteractive

#1.) Install Java 
RUN apt-get update && \
	apt-get install -y software-properties-common && \
	apt-get upgrade -y && \
   	apt-get install -y openjdk-8-jre-headless

#2.) Cleanup
RUN	apt-get clean && \
	find / -name *python* | xargs rm -rf && \
	rm -rf /tmp/* && \
	rm -rf /var/log/* 
	
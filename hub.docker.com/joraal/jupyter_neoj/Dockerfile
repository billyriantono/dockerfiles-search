FROM jupyter/datascience-notebook


USER root

RUN apt-get -y update && \
	apt-get -y upgrade && \
	apt-get install -y \
		software-properties-common unzip \
                ca-certificates \
                openssh-client \
                curl
				
# pip installs
RUN pip install py2neo

RUN pip install neo4j

RUN pip install Django


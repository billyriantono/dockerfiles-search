FROM ubuntu:latest

MAINTAINER simojenki

# Install dependencies
RUN apt-get update && \
    	apt-get install -y software-properties-common && \
	apt-add-repository ppa:ansible/ansible && \
	apt-get update && \
	apt-get -y install ansible && \
	rm -rf /var/lib/apt/lists/*


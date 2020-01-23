#+++++++++++++++++++++++++++++++++++++++
# Dockerfile for docker-python-pip 1.0
#    -- automatically generated  --
#+++++++++++++++++++++++++++++++++++++++


FROM webdevops/apache:ubuntu-16.04

RUN \
	sed -i 's|http://archive|http://us.archive|g' /etc/apt/sources.list && \
    apt-get update && \
    apt-get install -y software-properties-common python-software-properties && \
    apt-get install python-pip -y && \
    pip install bs4

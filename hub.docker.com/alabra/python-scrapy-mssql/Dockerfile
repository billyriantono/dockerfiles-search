# Pull base image.
FROM ubuntu:latest

# Install Python and prerequisites for pymssql and scrapy
RUN apt-get update && \
	apt-get -y upgrade && \
	apt-get install -y locales python python-dev python-pip libxml2-dev libxslt1-dev zlib1g-dev libffi-dev libssl-dev freetds-dev freetds-bin  && \
	apt-get clean && \
    rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN pip install pymssql && \
    pip install scrapy

# Define working directory.
WORKDIR /data

# Define default command.
CMD ["bash"]
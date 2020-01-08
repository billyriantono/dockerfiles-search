FROM ubuntu:trusty


RUN apt-get update && apt-get install -y --no-install-recommends \
		ca-certificates \
		curl \
		wget \
		unzip \
		mysql-client \
		libmysqlclient-dev \
        python-software-properties \
        software-properties-common \
	&& rm -rf /var/lib/apt/lists/*

RUN echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections
RUN echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections

RUN add-apt-repository -y ppa:webupd8team/java && apt-get update && apt-get install -y oracle-java7-installer \
    && rm -rf /var/lib/apt/lists/*

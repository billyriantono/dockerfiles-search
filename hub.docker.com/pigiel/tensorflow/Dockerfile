FROM ubuntu:bionic

# Install tools required in envrionment
RUN apt-get update && apt-get install -y \
	vim \
	python-pip \
# Delete all the apt list files to keep clean 
	&& rm -rf /var/lib/apt/lists/*

# Install python modules required in scripts
RUN pip --no-cache-dir install \
	scikit-learn \
	nltk \
	numpy \
	scipy \
	sklearn \
	matplotlib
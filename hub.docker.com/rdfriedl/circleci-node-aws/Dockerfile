FROM circleci/node:latest

ENV PATH /home/circleci/.local/bin:$PATH

RUN sudo apt-get install python groff less && \
	sudo curl -O https://bootstrap.pypa.io/get-pip.py && \
	sudo python get-pip.py --prefix=/usr/local && \
	sudo rm get-pip.py && \
	sudo apt-get update && \
	sudo apt-get install -y python-dev && \
	pip install awscli --upgrade --user && \
	aws configure set preview.cloudfront true

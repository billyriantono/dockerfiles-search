FROM ubuntu:latest
RUN apt-get update \
	&& apt-get install -y python-pip python-dev build-essential pandoc texlive-full \
	&& pip install --upgrade pip \
	&& pip install --upgrade virtualenv \
	&& pip install sphinx sphinx-autobuild sphinx_rtd_theme recommonmark

FROM jenkins/jenkins:latest

USER root

RUN apt-get update \
	&& apt-get install -y --no-install-recommends \
	gcc \
	g++ \
	gfortran \
	less \
	locales \
	libbz2-dev \
	libcairo2-dev \
	libcurl4-openssl-dev \
	libicu-dev \
	libjpeg-dev \
	libpcre3-dev \
	libpng-dev \
	libreadline-dev \
	libtiff5-dev \
	libx11-dev \
	libxt-dev \
	lmodern \
	tcl8.6-dev \
	texinfo \
	texlive-base \
	texlive-fonts-extra \
	texlive-fonts-recommended \
	texlive-latex-base \
	texlive-latex-recommended \
	tk8.6-dev \
	&& rm -rf /var/lib/apt/lists/*

USER jenkins

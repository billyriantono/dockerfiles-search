FROM asachet/rocker-ml:latest
LABEL maintainer="kosugitti@gmail.com"  \
org.label-schema.vcs-url="https://github.com/kosugitti/rstan-docker"

# Using clang to compile Stan
# Using the default g++ causes memory issues
RUN apt-get update \
&& apt-get install -y --no-install-recommends \
clang

# Install JAGS and other linux packages
RUN apt-get update && apt-get install -y \
	cargo \
	jags \
	gdal-bin \
	libudunits2-dev \
	libgsl0-dev \
	libprotobuf-dev \
	libglpk-dev \
	libcgal-dev \
	libglu1-mesa-dev \
	libgdal-dev \
	libproj-dev \
	libgeos-dev \
	openmpi-bin \
	proj-data \
	proj-bin \
	tcl8.6-dev \
	tk8.6-dev \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/*


# install_stan.R creates a makevars file and installs rstan from source
# following the instructions at https://github.com/stan-dev/rstan/wiki/Installing-RStan-on-Linux

COPY install_stan.R install_stan.R
RUN ["r", "install_stan.R"]

# Installing the rest 
RUN install2.r --skipinstalled --error --d TRUE --ncpus -1 \
	bayesplot \
	bridgesampling \
	brms \
	coda \
	GPArotation \
	loo \
	projpred \
	psych \
	rstanarm \
	rstantools \ 
	shinystan \
	summarytools \
	tidybayes \
	tidyverse \
	modeest \
	doRNG \
	lavaan \
	blavaan \
	formattable

RUN installGithub.r hoxo-m/pforeach --deps TRUE

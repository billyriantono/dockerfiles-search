#
# Build notes: from the provisioning/ directory, run:
#     docker build -t bce .
#
# Required files: (must be in working directory with Dockerfile)
# - userconf.sh (Docker only)
# - supervisord.conf (Docker only)
# - bootstrap-bce.sh (Generic BCE bash script)
# - setup_ipython_notebook.sh (Generic BCE scipt, does what it says)
#
# Usage notes:
# 
# Launch the image from any platform that has docker installed: 
# 
#     docker run -d -p 8787:8787 -p 2200:22 -p 8888:8888 -e USER=<username> -e PASSWORD=<password> --name bce cboettig/bce
# 
# If using boot2docker, look up `<ip-address>` with command: `boot2docker ip`. On a linux, `<ip-address>` is `localhost`.
#  
# - Connect to RStudio-server: go to `http://<ip-address>:8787` and log in with the user and password given.
# - Connect to an ssh session:  `ssh -p 2200 username@localhost`.  (Note, no root privileges)
# - Connect to an ipython session: go to `http://<ip-address>:8888`.  
# (Currently unsecured, do not expose an ipython port on a public host/cloud machine)
# 



FROM ubuntu:14.04 
MAINTAINER Carl Boettiger <cboettig@ropensci.org>

ENV DEBIAN-FRONTEND noninteractive
ENV LC_ALL en_US.UTF-8

## Not sure why the shell script isn't installing these?
RUN apt-get update && apt-get install -y \
  ed \
  libxml2 \
  libxslt1-dev \
  python-pip \
  libjpeg62 \
  libcurl4-openssl-dev \
  r-cran-rjava \
  dnsutils

## Generate the appropriate UTF-8 locale
RUN locale-gen en_US.UTF-8

## Get additional build dependencies to avoid pip-install failures...
RUN apt-get build-dep -y python-matplotlib

## Copy over the BCE scripts and bootstrap ##
COPY packages /tmp/packages
COPY bootstrap-bce.sh /usr/bin/bootstrap-bce.sh
RUN chmod a+x /usr/bin/bootstrap-bce.sh
RUN /usr/bin/bootstrap-bce.sh


## RStudio-Server setup
ENV VER 0.98.1080   
RUN echo "deb http://archive.ubuntu.com/ubuntu trusty-backports main restricted universe" >> /etc/apt/sources.list \
&& apt-get update && apt-get install -y -q \
   libapparmor1 \
   libssl0.9.8 \
   psmisc \
   supervisor \
   sudo \
&& wget -q http://ftp.us.debian.org/debian/pool/main/o/openssl/libssl0.9.8_0.9.8o-4squeeze14_amd64.deb \ 
&& dpkg -i libssl0.9.8_0.9.8o-4squeeze14_amd64.deb && rm libssl0.9.8_0.9.8o-4squeeze14_amd64.deb \
&& (wget -q https://s3.amazonaws.com/rstudio-server/current.ver -O currentVersion.txt \
&& VER=$(cat currentVersion.txt) \
&& wget -q http://download2.rstudio.org/rstudio-server-${VER}-amd64.deb \
&& dpkg -i rstudio-server-${VER}-amd64.deb \
&& rm rstudio-server-*-amd64.deb currentVersion.txt) \
&& ln -s /usr/lib/rstudio-server/bin/pandoc/pandoc /usr/local/bin \
&& ln -s /usr/lib/rstudio-server/bin/pandoc/pandoc-citeproc /usr/local/bin

## This shell script is executed by supervisord when it is run by CMD, configures env variables
ADD userconf.sh /usr/bin/userconf.sh

## Set up ssh
RUN apt-get update && apt-get install -y \
    openssh-server \
  && mkdir /var/run/sshd


## Create a default user
RUN useradd swc

## Expose default ports for external services. (Must be linked a runtime)
## as follows: RStudio: 8787, ipython-notebook: 8888, ssh: 22 
EXPOSE 8787
EXPOSE 8888
EXPOSE 22

## Secure ipython notebook setup
## Currently this requires logging into the session and running 
## `setup_ipython_notebook` interactively. Even so, doesn't seem
## to be working for me.  
COPY setup_ipython_notebook.sh /usr/bin/setup_ipython_notebook
RUN chmod a+x /usr/bin/setup_ipython_notebook
EXPOSE 9999

## To have a container run multiple & persistent tasks, we use the 
## very simple supervisord as recommended in Docker documentation.
RUN mkdir -p /var/log/supervisor
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
CMD ["/usr/bin/supervisord"] 


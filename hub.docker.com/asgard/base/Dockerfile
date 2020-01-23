# Base
FROM phusion/baseimage:0.9.15


###########################################################################
# Regular system stuff
###########################################################################

RUN apt-get -y update \
  && apt-get -y upgrade \
  && apt-get -y install git-core build-essential gfortran \
  && apt-get -y install python-pip \
  && apt-get install -y --no-install-recommends software-properties-common \
  && apt-get install -y sqlite3

###########################################################################
# Init Setup Script
###########################################################################

ADD init_script /sbin/init_script

# au cas ou
# RUN chmod +x init_script
ENTRYPOINT ["/sbin/init_script"]

# Clean up APT when done.
RUN apt-get clean  \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*



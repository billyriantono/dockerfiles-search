############################################################
# Dockerfile to build a NodeJS v5 Base Container
# Based on: appcontainers/debian
# DATE: 12/30/2015
# COPYRIGHT: Appcontainers.com
############################################################

# Set the base image in namespace/repo format.
# To use repos that are not on the docker hub use the example.com/namespace/repo format.
FROM appcontainers/debian

# File Author / Maintainer
MAINTAINER Rich Nason rnason@appcontainers.com

###################################################################
#*************************  Reset Apache CTN  *********************
###################################################################


###################################################################
#*************************  APP VERSIONS  *************************
###################################################################


###################################################################
#***************  OVERRIDE ENABLED ENV VARIABLES  *****************
###################################################################

ENV TERMTAG NODEJS

###################################################################
#******************  ADD REQUIRED APP FILES  **********************
###################################################################

###################################################################
#*******************  UPDATES & PRE-REQS  *************************
###################################################################

# Update and install wget, so we can get the key
RUN apt-get clean all && \
apt-get -y update && \
DEBIAN_FRONTEND=noninteractive apt-get -y upgrade && \
DEBIAN_FRONTEND=noninteractive apt-get -y install wget

# Get the appcontainers repository in order to grab the nodeJS build
RUN wget -qO - http://apt.appcontainers.io/APPCONTAINERS-GPG-KEY.public | apt-key add - && \
echo 'deb [arch=amd64] http://apt.appcontainers.io jessie main' >> /etc/apt/sources.list

###################################################################
#**********************  CENTOS/RHEL  *****************************
###################################################################

# Clean, Update, and Install... then clear non English local data.
RUN apt-get clean all && \
apt-get -y update && \
DEBIAN_FRONTEND=noninteractive apt-get -y install nodejs tar curl && \
apt-get clean && \
rm -fr /var/lib/apt/lists/*


###################################################################
#*******************  APPLICATION INSTALL  ************************
###################################################################

# Doing an npm install npm@3 -g fails with "EXDEV: cross-device link not permitted"
RUN npm cache clear && npm -v && \
ln -s /usr/bin/node /usr/bin/nodejs && \
curl -L https://npmjs.org/install.sh | sh && \
npm -v

###################################################################
#******************  POST DEPLOY CLEAN UP  ************************
###################################################################


###################################################################
#*****************  CONFIGURE START ITEMS  ************************
###################################################################


###################################################################
#****************  EXPOSE APPLICATION PORTS  **********************
###################################################################

EXPOSE 3000

###################################################################
#*******************  OPTIONAL / LEGACY  **************************
###################################################################

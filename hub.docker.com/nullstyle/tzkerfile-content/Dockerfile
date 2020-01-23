FROM dockerfile/java:oracle-java7
 
MAINTAINER Tom Jackson thomas.jackson@nordstrom.com

# define env variables that will allow all atlassian app image builds to navigate the 
# outbound proxy 
# ENV http_proxy http://pbcld-proxy.nordstrom.net:3128
# ENV https_proxy https://pbcld-proxy.nordstrom.net:3128 
# ENV no_proxy localhost,10.0.0/8,nordstrom.net

# Use a Dynatrace agent for JVM monitoring of Java-based Atlassian apps

# dynatrace Agent URL
ENV  AGENT_URL  https://bitbucket.org/nordstrom-sets/atlassian-app/downloads

# agent version
ENV AGENT_VERSION 6.0.0.6738

# agent install path
ENV AGENT_INSTALL /usr/local/dynatrace

ENV AGENT_PATH ${AGENT_INSTALL}/agent/lib64/libdtagent.so


# Install xmlstarlet for use in manipulating xml files in situ
# Ability is useful for Atlassian apps that use an xml file to configure the DB
# connection but do not support variables in the files.
RUN set -x \
    && apt-get update --quiet \
    && apt-get install --quiet --yes --no-install-recommends libtcnative-1 xmlstarlet

# Install VIM so we have at least some editing capability
sudo apt-get install vim

# Install zip/unzip for troubleshooting purposes (creating and copying archives to/from server)
apt-get install zip
apt-get install unzip

# change to a temp directory
WORKDIR /tmp

# get the agent jar
RUN wget ${AGENT_URL}/dynatrace-agent-${AGENT_VERSION}-linux.jar

# install agent under /usr/local
WORKDIR /usr/local/

# install the agent

# installer is a executable jar
# installer prompts with the following question:
# 1) do you want to install it here? (Y/N)
# enter a 'Y' followed by a CR
# 
# the result will be an agent installed under:
# /usr/local/dynatrace-6.0.0

RUN printf 'Y\n' | java -jar /tmp/dynatrace-agent-6.0.0.6738-linux.jar

# rename the directory to just 'dynatrace'
RUN mv /usr/local/dynatrace-6.0.0 /usr/local/dynatrace

# add a version file so the agent version is still clear
RUN touch /usr/local/dynatrace/version.txt
RUN echo ${AGENT_VERSION} > /usr/local/dynatrace/version.txt

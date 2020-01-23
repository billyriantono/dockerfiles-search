################################################################################
#                                                                              #
#                                 {o,o}                                        #
#                                 |)__)                                        #
#                                 -"-"-                                        #
#                                                                              #
################################################################################
#
# Prerender docker image
#
##################################---BASE---####################################

FROM debian:latest

################################################################################

###############################---MAINTAINER---#################################

MAINTAINER Price Pilot <hello@pricepilot.io>

################################################################################

##################################---ENV---#####################################

ENV DEBIAN_FRONTEND noninteractive
ENV PORT 3000

################################################################################

#################################---BUILD---####################################

RUN apt-get update; \
    apt-get upgrade --yes; \
    apt-get install --yes \
        git \
        curl \
        wget \
        vim \
        gnupg2

#install node including npm
RUN ln -s /usr/bin/nodejs /usr/bin/node; \
    curl -sL https://deb.nodesource.com/setup_9.x | bash - ;\
    apt-get install -y -q nodejs;

#install chromium
RUN wget https://dl.google.com/linux/direct/google-chrome-beta_current_amd64.deb; \
    dpkg -i google-chrome-beta_current_amd64.deb; \
    apt-get -fyq install;

#install prerender
RUN git clone https://github.com/mimazoo/prerender /opt/prerender
WORKDIR /opt/prerender
RUN npm install

EXPOSE $PORT

################################################################################

################################---COMMAND---###################################

CMD node server.js

################################################################################

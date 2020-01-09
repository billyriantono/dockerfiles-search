FROM clouder/clouder-nginx
MAINTAINER Yannick Buron yburon@goclouder.net

RUN touch /tmp/magento-ssh
RUN apt-get -qq update && DEBIAN_FRONTEND=noninteractive apt-get -y -qq install openssh-server
USER root

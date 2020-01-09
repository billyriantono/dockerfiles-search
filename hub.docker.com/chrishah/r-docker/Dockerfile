FROM ubuntu:18.04

MAINTAINER <christoph.hahn@uni-graz.at>

#RUN apt-get update && apt-get -y upgrade && apt-get install -y build-essential vim git wget

#Install R (R installation asks for timezone interactively so this needs to be switched off and set before)
ENV DEBIAN_FRONTEND noninteractive
ENV DEBCONF_NONINTERACTIVE_SEEN true
## preesed tzdata, update package index, upgrade packages and install needed software
# and finally ggplot2 with all dependencies
RUN echo "tzdata tzdata/Areas select Europe" > /tmp/preseed.txt; \
	echo "tzdata tzdata/Zones/Europe select Vienna" >> /tmp/preseed.txt; \
	debconf-set-selections /tmp/preseed.txt && \
	apt-get update && \
	apt-get install -y tzdata r-base && \
	R --vanilla -e 'install.packages("ggplot2", repos="http://cran.wu.ac.at/")'


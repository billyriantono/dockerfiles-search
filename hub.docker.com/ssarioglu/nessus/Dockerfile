FROM debian:latest

MAINTAINER Serdar Sarioglu, Serdar.Sarioglu@mysystem.org

#This will be used for Licence Mapping
ENV LICENCE AddYourLicenceHere

#Install Nessus
RUN apt-get update && apt-get install -y wget
RUN wget -O nessus.deb --user-agent='Mozillqa/5.0 (Windows NT 10.0; WOW64; rv:48.0) Gecko/20100101 Firefox/48.0' --header='Upgrade-Insecure-Requests: 1' 'https://s3.eu-central-1.amazonaws.com/grafclouds/iso/Nessus-8.1.1-debian6_amd64.deb'
RUN dpkg -i nessus.deb && rm nessus.deb

EXPOSE 8834

ENTRYPOINT ["/opt/nessus/sbin/nessusd"]

VOLUME ["/opt/nessus/etc/nessus/"]

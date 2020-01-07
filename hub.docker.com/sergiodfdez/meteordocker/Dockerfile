#Base Image
FROM ubuntu:latest
MAINTAINER "Sergio D Fdez <sergiodfdez@gmail.com>"

#Update and Upgrade
RUN apt-get update && apt-get -y upgrade

#Install curl
RUN apt-get install -y curl

#Intall Meteor
curl https://install.meteor.com/ | sh
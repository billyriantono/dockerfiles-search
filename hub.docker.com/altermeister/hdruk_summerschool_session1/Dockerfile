# We will use Ubuntu for our image
FROM continuumio/anaconda3:latest

# Updating Ubuntu packages
# RUN apt-get update && apt-get install -y --no-install-recommends apt-utils
RUN apt-get update && yes|apt-get upgrade
RUN apt-get install -y emacs


# # Adding wget and bzip2 and python and pip
RUN apt-get install -y wget bzip2 python3-pip python3

# # Add sudo
RUN apt-get -y install sudo

# # Add user hdruk with no password, add to sudo group
RUN adduser --disabled-password --gecos '' hdruk
RUN adduser hdruk sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
USER hdruk
WORKDIR /home/hdruk/
RUN chmod a+rwx /home/hdruk/
RUN echo `pwd`

FROM    ubuntu:14.04

RUN ["apt-get", "install", "--force-yes", "-y", "pkg-config", "software-properties-common", "python-setuptools"]
# Enable chris-lea PPA
RUN     add-apt-repository -y ppa:chris-lea/node.js
# Refresh the system
RUN ["apt-get", "update"]
RUN ["apt-get", "-qy", "upgrade"]
RUN ["apt-get", "clean"]
# Install packages
RUN ["apt-get", "install", "--force-yes", "-qy", "curl", "wget", "unzip", "build-essential", "cmake", "cython", "python2.7-dev", "nodejs", "ruby"]

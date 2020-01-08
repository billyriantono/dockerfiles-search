FROM itriage/base:latest
MAINTAINER Itriage Ops <ops@itriagehealth.com>

# Pull and install node.js
RUN DEBIAN_FRONTEND=noninteractive apt-get update
RUN apt-get install -y g++ make python
RUN DEBIAN_FRONTEND=noninteractive add-apt-repository ppa:chris-lea/node.js
RUN DEBIAN_FRONTEND=noninteractive apt-get update
RUN apt-get install -y nodejs


RUN adduser --home /home/ubuntu ubuntu

ONBUILD ADD . /mnt/app
ONBUILD RUN ["chown", "-R", "ubuntu", "/mnt/app"]

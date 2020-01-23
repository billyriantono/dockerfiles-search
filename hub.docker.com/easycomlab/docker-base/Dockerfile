FROM debian:jessie
MAINTAINER EasycomLab <easycomlab@easycom.digital>

# Add the bashrc configuration
ADD ./bashrc.root /root/.bashrc

RUN DEBIAN_FRONTEND=noninteractive apt-get update
RUN apt-get -y --no-install-recommends install nano vim htop iptraf git

CMD /bin/bash -i

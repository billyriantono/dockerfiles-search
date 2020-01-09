# Base image for Xpra based GUI containers
#

FROM ubuntu:14.04
MAINTAINER Assaf Berg <aberg@vmware.com>
RUN apt-get update && apt-get install -y \
	curl \
	lxterminal \
	nano \
	python-software-properties \
	software-properties-common \
	vim \
	xpra \
	xterm

# create user
RUN useradd -b /home -s /bin/bash -m -g users user
RUN echo "user ALL=NOPASSWD: ALL" >> /etc/sudoers

USER user
ENV HOME /home/user
RUN echo "export DISPLAY=:70" >> $HOME/.profile

ENTRYPOINT [ "/usr/bin/xpra" ]
CMD [ "start", ":70", \
	"--no-daemon", "--no-speaker", "--no-microphone", "--no-pulseaudio", \
	"--start-child=/usr/bin/lxterminal --working-directory=$HOME" ]

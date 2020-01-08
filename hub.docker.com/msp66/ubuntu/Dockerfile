FROM ubuntu:18.04
LABEL edu.uanet.msp66-devops.url="https://github.com/facetoe/terminote2" \
	edu.uanet.msp66-devops.distro="ubuntu" \
	edu.uanet.msp66-devops.osversion="18.04" \
	edu.uanet.msp66-devops.architecture="x86_64"

#Update and install dependencies
RUN apt-get update -y && apt-get install -y \
	make \
	g++ \
	git \
	libncurses5-dev \
	libncursesw5-dev

#Download source code
ARG NOTE_URL="https://github.com/facetoe/terminote2.git"
RUN git clone $NOTE_URL

#Compile and make source code
RUN cd terminote2/src && make

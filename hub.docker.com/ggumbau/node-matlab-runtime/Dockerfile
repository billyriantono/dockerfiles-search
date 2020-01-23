FROM node:latest
RUN apt-get update -y
RUN apt-get install unzip -y
RUN mkdir /mcr-install && cd /mcr-install && \
	wget https://www.mathworks.com/supportfiles/downloads/R2017a/deployment_files/R2017a/installers/glnxa64/MCR_R2017a_glnxa64_installer.zip && \
	unzip MCR_R2017a_glnxa64_installer.zip && \
	./install -mode silent -agreeToLicense yes
RUN rm -Rf /mcr-install

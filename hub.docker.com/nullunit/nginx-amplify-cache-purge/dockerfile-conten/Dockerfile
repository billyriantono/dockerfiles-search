FROM python:2.7.9
 
MAINTAINER Tom Jackson thomas.jackson@nordstrom.com

# define env variables that will allow all provisioners to navigate the 
# outbound proxy 
# ENV http_proxy http://pbcld-proxy.nordstrom.net:3128
# ENV https_proxy https://pbcld-proxy.nordstrom.net:3128 
# ENV no_proxy localhost,10.0.0/8,nordstrom.net

# define install dir
ENV READONLY_INSTALL  /usr/local/readonly-confluence

# install docker-py and schedule modules
RUN pip install docker-py
RUN pip install schedule

# Add the readonly scripts to install directory
RUN mkdir -p ${READONLY_INSTALL}/src 
ADD src/  ${READONLY_INSTALL}/src/

RUN mkdir ${READONLY_INSTALL}/lib 
ADD lib/  ${READONLY_INSTALL}/lib/

# Run under the root account by not declaring USER here. 
# This is a requirement as the container leverages the Docker Remote API

# Set the working directory to the backup-install directory
WORKDIR ${READONLY_INSTALL}

# launch the readonly service in foreground
CMD python -m src.readonly_server

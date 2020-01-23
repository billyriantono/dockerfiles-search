FROM python:2.7.9
 
MAINTAINER Tom Jackson thomas.jackson@nordstrom.com

# define env variables that will allow all provisioners to navigate the 
# outbound proxy 
# ENV http_proxy http://pbcld-proxy.nordstrom.net:3128
# ENV https_proxy https://pbcld-proxy.nordstrom.net:3128 
# ENV no_proxy localhost,10.0.0/8,nordstrom.net

# define install dir
ENV CONFIGS_INSTALL  /usr/local/confluence-configs

# Port to run the readme server on
ENV SERVER_PORT 8090

# install required python packages
RUN pip install mysql-connector-python --allow-external mysql-connector-python
RUN easy_install lxml
RUN easy_install web.py

RUN pip install Jinja2
RUN pip install MarkupSafe
RUN pip install SQLAlchemy
RUN pip install jprops
RUN pip install requests

# Install VIM so we have at least some editing capability inside container
RUN apt-get update --quiet
RUN printf 'Y' | apt-get install vim

# Add scripts and config file to configs-install directory
RUN mkdir ${CONFIGS_INSTALL}
RUN mkdir ${CONFIGS_INSTALL}/src
RUN mkdir ${CONFIGS_INSTALL}/lib
RUN mkdir ${CONFIGS_INSTALL}/config

ADD src/     ${CONFIGS_INSTALL}/src/
ADD lib/     ${CONFIGS_INSTALL}/lib/
ADD config/  ${CONFIGS_INSTALL}/config/

# Set the working directory to the configs-install directory
WORKDIR ${CONFIGS_INSTALL}

# run server in the foreground
# main purpose of server is make the container long running, so the utilities it provides
# can be run via the container name/alias (using docker exec ...) instead of via the image 
# (using docker run ...), which is more cumbersome
CMD python src/readme.py $SERVER_PORT
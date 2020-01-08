############################################################
# Dockerfile to build Vib App docker image
# Based on ryanrhymes/vib_app master branch
# By Liang Wang <liang.wang@cl.cam.ac.uk>
############################################################

FROM nginx:latest


##################### PREREQUISITES ########################

RUN apt-get update
RUN apt-get -y install git wget unzip aspcud m4 pkg-config
RUN apt-get -y install build-essential

RUN wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
ENV NVM_DIR /root/.nvm
RUN [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" && nvm install node


####################   INSTALL VIB  #######################

ENV VIBPATH /vib_app
RUN git clone https://github.com/ryanrhymes/vib_app.git
RUN [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" && make -C $VIBPATH


####################   SETUP NGINX  #######################

RUN cp -r $VIBPATH/build/* /usr/share/nginx/html/

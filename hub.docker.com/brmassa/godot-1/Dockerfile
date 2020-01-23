FROM ubuntu:latest

# Variables
ARG GODOT_VERSION=3.0
ARG GODOT_VARIANT=rc1
ARG GODOT_SUBFOLDER=rc1/
#ARG GODOT_MONO=mono/

# Setup the system 
#RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections
RUN apt-get update \ 
    && apt-get upgrade -y \ 
    && apt-get install -y -qq wget unzip software-properties-common libx11-6 sudo zip \
    && mkdir -p /opt/

# Download Godot
RUN cd /opt \
    && wget -q -O godot.zip https://downloads.tuxfamily.org/godotengine/${GODOT_VERSION}/${GODOT_SUBFOLDER}Godot_v${GODOT_VERSION}-${GODOT_VARIANT}_x11.64.zip \
    && unzip godot.zip

# Download export templates
RUN cd /opt \
    && wget -q -O templates.zip https://downloads.tuxfamily.org/godotengine/${GODOT_VERSION}/${GODOT_SUBFOLDER}Godot_v${GODOT_VERSION}-${GODOT_VARIANT}_export_templates.tpz \
    #&& mv Godot_v${GODOT_VERSION}-${GODOT_VARIANT}_export_templates.tpz Godot_v${GODOT_VERSION}-${GODOT_VARIANT}_export_templates.zip \
    && unzip templates.zip \
    && mkdir ~/.godot/ \
    && mv templates ~/.godot/ 
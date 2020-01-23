################# BASE IMAGE ######################
FROM binfgsc/base:latest

################## METADATA #######################
LABEL base.image="binfgsc/base:latest"
LABEL about.summary="A base image running programs that require java"

################## MAINTAINER #####################
LABEL maintainer.name="William Hargreaves"
LABEL maintainer.email="whargrea@uoguelph.ca"

################# INSTALLATION ####################
# install jre 
RUN sudo apk update && \
    sudo apk add --no-cache openjdk8-jre
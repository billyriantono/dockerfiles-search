FROM jenkins/jenkins:lts

# add the packages you need here
# packages for python/pip builds
ENV PYTHON_PACKAGES gcc python-dev libjpeg-dev zlib1g-dev libxml2-dev libxslt1-dev bzip2 build-essential python3 python3-dev
# others things needed for this jenkins installation
ENV ADDITIONAL_PACKAGES locales lftp

USER root
# install gcc for stuff that needs to be built (e.g. image stuff in python)
RUN apt-get update && apt-get install -y $PYTHON_PACKAGES $ADDITIONAL_PACKAGES

# let generate some locales
RUN sed -i 's/# en_US/en_US/' /etc/locale.gen
RUN locale-gen
ENV LANG en_US.UTF-8  
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8  

USER jenkins

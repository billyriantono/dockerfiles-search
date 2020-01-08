FROM jupyter/base-notebook

# Install Java Kernel
USER root
RUN echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" | tee /etc/apt/sources.list.d/webupd8team-java.list && \
       echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" | tee -a /etc/apt/sources.list.d/webupd8team-java.list && \
       apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886 && \
       apt-get update
RUN echo debconf shared/accepted-oracle-license-v1-1 select true | sudo debconf-set-selections && \
       echo debconf shared/accepted-oracle-license-v1-1 seen true | sudo debconf-set-selections
RUN apt-get install -y git oracle-java9-installer

USER $NB_USER
WORKDIR /home/jovyan
RUN git clone https://github.com/SpencerPark/jupyter-jvm-basekernel.git --depth 1 ./jupyter-jvm-basekernel && \
       cd jupyter-jvm-basekernel && ls -al
WORKDIR /home/jovyan/jupyter-jvm-basekernel
RUN echo "Currently (should be /home(jovyan/jupyter-jvm-basekernel) in $(pwd)"
RUN echo $(ls -al)
RUN chmod u+x gradlew
RUN ./gradlew publishToMavenLocal && cd /home/jovyan

RUN cd /home/jovyan

WORKDIR /home/jovyan

RUN git clone https://github.com/SpencerPark/IJava.git --depth 1 && \
       cd IJava/

WORKDIR /home/jovyan/IJava
RUN chmod u+x ./gradlew
RUN ./gradlew installKernel

RUN mkdir ~/notebooks

WORKDIR /home/jovyan/notebooks
VOLUME /home/jovyan/notebooks

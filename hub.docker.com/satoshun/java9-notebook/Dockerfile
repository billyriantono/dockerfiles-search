FROM satoshun/jupyter

MAINTAINER SatoShun <shun.sato1@gmail.com>

ENV KULLA_VERSION kulla--20160124010109
ENV KULLA_HOME /usr/bin/kulla.jar
ENV JAVA_9_HOME /usr
USER root

# java9 install
RUN echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" | tee /etc/apt/sources.list.d/webupd8team-java.list && \
        echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" | tee -a /etc/apt/sources.list.d/webupd8team-java.list && \
        apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886 && \
        apt-get clean && \
        apt-get update -y && \
        apt-get upgrade -y && \
        apt-get install -y apt-utils

# License agreement
RUN echo debconf shared/accepted-oracle-license-v1-1 select true | \
        debconf-set-selections
RUN echo debconf shared/accepted-oracle-license-v1-1 seen true | \
        debconf-set-selections

RUN apt-get install -yq oracle-java9-installer && \
        apt-get install -yq oracle-java9-set-default git

# install KULLA
RUN wget https://adopt-openjdk.ci.cloudbees.com/view/OpenJDK/job/langtools-1.9-linux-x86_64-kulla-dev/351/artifact/${KULLA_VERSION}.jar -O ${KULLA_VERSION}.jar && \
        cp ${KULLA_VERSION}.jar ${KULLA_HOME}

# create
RUN git clone https://github.com/Bachmann1234/java9_kernel.git ${HOME}/java9_kernel
RUN mkdir -p ${HOME}/.ipython/kernels/java/
RUN echo "{ \n\
    \"argv\": [\"python3\", \"${HOME}/java9_kernel/javakernel\", \n\
             \"-f\", \"{connection_file}\"], \n\
    \"display_name\": \"Java 9\", \n\
    \"language\": \"java\", \n\
    \"env\" : { \n\
        \"JAVA_9_HOME\": \"${JAVA_9_HOME}\", \n\
        \"KULLA_HOME\": \"${KULLA_HOME}\" \n\
    } \n\
}" > ${HOME}/.ipython/kernels/java/kernel.json

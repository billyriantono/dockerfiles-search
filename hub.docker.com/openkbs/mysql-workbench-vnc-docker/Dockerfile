FROM openkbs/jdk-mvn-py3-vnc

MAINTAINER DrSnowbird "DrSnowbird@openkbs.org"

## -------------------------------------------------------------------------------
## ---- USER is defined in parent image: openkbs/jdk-mvn-py3-vnc already ----
## -------------------------------------------------------------------------------
ENV USER=${USER:-developer}
ENV HOME=/home/${USER}
ENV WORKSPACE=${HOME}/workspace
ENV DATA=${HOME}/data

#### ---- MYSQL Setup ----
ENV MYSQL_REPO=https://dev.mysql.com/get/Downloads/MySQLGUITools
ENV MYSQL_WORKBENCH_VERSION=${MYSQL_WORKBENCH_VERSION:-6.3.10-1ubuntu16.04-amd64}
ENV MYSQL_WORKBENCH_WORKBENCH=${MYSQL_WORKBENCH_WORKBENCH:-mysql-workbench-community-6.3.10-1ubuntu16.04-amd64.deb}

RUN sudo apt-get update && \
    sudo apt-get install -y mysql-workbench 
    #curl -L ${MYSQL_REPO}/${MYSQL_WORKBENCH_DEBIAN} > /tmp/${MYSQL_WORKBENCH_PACKAGE} && \
    #dpkg -i /tmp/${MYSQL_PACKAGE} && \
    #rm -f /tmp/${MYSQL_PACKAGE} 

RUN sudo apt-get install -y libproj-dev gnome-keyring

VOLUME ${WORKSPACE}
VOLUME ${DATA}

RUN mkdir -p ${WORKSPACE} ${DATA} && \
    sudo chown -R ${USER}:${USER} ${WORKSPACE} ${DATA}

##################################
#### VNC ####
##################################
WORKDIR ${HOME}

COPY ./vnc_startup.sh /dockerstartup/vnc_startup2.sh

USER ${USER}
ENTRYPOINT ["/dockerstartup/vnc_startup2.sh"]

##################################
#### Set up user environments ####
##################################

CMD ["/usr/bin/mysql-workbench"]


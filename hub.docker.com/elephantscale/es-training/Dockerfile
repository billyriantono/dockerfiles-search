# dockerfile for training image

FROM ubuntu:bionic

# args for docker file
ARG MYUSER=ubuntu
ARG DEFAULT_PASSWORD=bingobob123
ARG USER_GROUP_ID=1000
ARG HOME_DIR=/home/${MYUSER}
ARG APPS_DIR=${HOME_DIR}/apps
ARG CONDA_DIR=${APPS_DIR}/anaconda
ARG NVM_VERSION=0.34.0
ARG R_STUDIO_SERVER_VERSION=1.2.1335

# envs for the runtime container
ENV NVM_DIR         ${APPS_DIR}/nvm
ENV NODE_VERSION    10.16.0
ENV ES_HOME         ${HOME_DIR}
ENV NODE_PATH       ${NVM_DIR}/v${NODE_VERSION}/lib/node_modules
ENV PATH            ${NVM_DIR}/versions/node/v${NODE_VERSION}/bin:${PATH}
ENV SHELL           /bin/bash
ENV USER            ${MYUSER}

## for apt to be noninteractive
ENV DEBIAN_FRONTEND noninteractive
ENV DEBCONF_NONINTERACTIVE_SEEN true

RUN echo "*** http_proxy=${http_proxy} ***"

## ROOT level installs
## update all system
RUN apt update --fix-missing -yq && \
        apt -yq upgrade

## basic utils
RUN apt update && \
    apt install -yq  --no-install-recommends \
        atop \
        build-essential \
        ca-certificates \
        curl \
        git \
        gnupg \
        gnupg1 \
        gnupg2 \
        jq \
        less \
        nano \
        netcat \
        rsync \
        screen \
        sudo \
        unzip \
        vim \
        wget \
        zip


## Services
RUN apt update && \
    apt install -yq  --no-install-recommends \
        ntp  \
        openssh-server \
        openssh-client



## Install R
## This is a very time consuming step.
## So do it early so not to bust cache
RUN apt update && \
    apt -y install  libcurl4-openssl-dev  r-base  r-base-dev

# updating R packages
# RUN R -e "update.packages(ask = FALSE , repos = 'http://cran.us.r-project.org')"
#RUN R -e "install.packages('ggplot2' , repos = 'http://cran.us.r-project.org')"
RUN R -e "install.packages('tidyverse' , repos = 'http://cran.us.r-project.org')"

## ------ Install Rstudio
RUN apt update && \
    apt install -y   libclang-dev   psmisc  lsb-release
RUN wget  --quiet "https://elephantscale-public.s3.amazonaws.com/downloads/rstudio-server-${R_STUDIO_SERVER_VERSION}-amd64.deb" && \
        dpkg -i  rstudio-server-${R_STUDIO_SERVER_VERSION}-amd64.deb && \
        rm -f rstudio-server*.deb


## --- VNC Server  (see user mode installs below for noVNC)
RUN apt update && \
    apt install -y  xfce4 xfce4-goodies tightvncserver

######## start: monitoring stack (graphite, graphana, statsd) ######
## --- Mysql
RUN apt update && \
    apt install -yq \
        mysql-server \
        python-mysqldb \
        python-pymysql
RUN mkdir /var/run/mysqld

## create databases
RUN chown -R mysql:mysql /var/lib/mysql /var/run/mysqld && \
    service mysql start && \
    mysql -u root -e "create database graphite;" && \
    mysql -u root -e "grant all privileges on graphite.* to 'graphite'@'%'  identified by '${DEFAULT_PASSWORD}';" &&\
    mysql -u root -e "create database grafana;" && \
    mysql -u root -e "grant all privileges on grafana.* to 'graphite'@'%'  identified by '${DEFAULT_PASSWORD}';"

## --- Apache web server
RUN apt update && \
    apt install -y \
        apache2 \
        libapache2-mod-wsgi &&  \
    a2enmod wsgi
COPY ./config/apache-ports.conf  /etc/apache2/ports.conf
COPY ./config/apache-000-default.conf /etc/apache2/sites-available/000-default.conf


## Install Grafana
RUN curl https://packages.grafana.com/gpg.key | sudo apt-key add - && \
	apt install -y software-properties-common && \
	add-apt-repository "deb https://packages.grafana.com/oss/deb stable main" && \
	apt update && \
	apt install -y grafana
COPY ./config/grafana.ini    /etc/grafana/grafana.ini

## Install Graphite
RUN sudo apt -y install python-dev python-pip libcairo2-dev libffi-dev build-essential && \
	export PYTHONPATH="/opt/graphite/lib/:/opt/graphite/webapp/" && \
	sudo -H pip install --no-binary=:all: https://github.com/graphite-project/whisper/tarball/master && \
	sudo -H pip install --no-binary=:all: https://github.com/graphite-project/carbon/tarball/master && \
	sudo -H pip install --no-binary=:all: https://github.com/graphite-project/graphite-web/tarball/master

RUN sudo -H PYTHONPATH=/opt/graphite/webapp django-admin.py migrate --settings=graphite.settings --run-syncdb
RUN sudo -H PYTHONPATH=/opt/graphite/webapp django-admin.py createsuperuser --settings=graphite.settings
RUN sudo -H PYTHONPATH=/opt/graphite/webapp django-admin.py collectstatic --noinput --settings=graphite.settings
RUN cp /opt/graphite/conf/carbon.conf.example /opt/graphite/conf/carbon.conf  && \
        cp /opt/graphite/conf/storage-schemas.conf.example /opt/graphite/conf/storage-schemas.conf
COPY ./config/graphite.wsgi  /opt/graphite/conf/graphite.wsgi
RUN chmod +x /opt/graphite/conf/graphite.wsgi  && \
	chown -R www-data:www-data /opt/graphite
COPY ./config/graphite-vhost.conf  /etc/apache2/sites-available/graphite-vhost.conf
RUN a2dissite 000-default && \
	a2ensite graphite-vhost

## Install Statsd
RUN curl -L -s https://deb.nodesource.com/setup_10.x | sudo bash  && \
        apt install -y nodejs  && \
        git clone https://github.com/etsy/statsd.git /opt/statsd
COPY ./config/statsd-localConfig.js  /opt/statsd/localConfig.js

## Set up Supervisor

RUN sudo apt install -y supervisor
COPY ./config/statsd.conf  /etc/supervisor/conf.d/statsd.conf
COPY ./config/carbon.conf  /etc/supervisor/conf.d/carbon.conf


######## end: monitoring stack (graphite, graphana, statsd) ######


## --- JDK
RUN apt update && \
    apt install -yq openjdk-8-jdk

## --- Scala and SBT
RUN echo "deb https://dl.bintray.com/sbt/debian /" >  /etc/apt/sources.list.d/sbt.list && \
    apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2EE0EA64E40A89B84B2DF73499E82A75642AC823 && \
    apt update && \
    apt install -y  sbt scala

## --- install a browser
#RUN apt install -y chromium-browser
RUN apt install -y firefox

## Ip utils
RUN sudo apt install -y \
    iputils-ping \
    iproute2 \
    netcat-traditional\
    netcat-openbsd\
    nmap

## --- cleanup apt
## delete proxy
RUN rm -f /etc/apt/apt.conf.d/01proxy  && \
        apt clean && \
        rm -rf /var/lib/apt/lists/*

## --- config SSH : Preventing SSH timeouts + enable password login
RUN cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak
COPY ./config/sshd_config  /etc/ssh/sshd_config

## ======== USER land  =======

## --- Create ubuntu user and home dir
## Do this before any user installs
RUN groupadd -g ${USER_GROUP_ID} ${MYUSER} && \
    useradd -rm -d ${HOME_DIR} -s /bin/bash -g ${MYUSER} -G sudo -u ${USER_GROUP_ID} ${MYUSER}


# make sure user owns his home dir
RUN mkdir -p ${HOME_DIR}  && \
    chown -R ${MYUSER} ${HOME_DIR}


## disable sudo password
## https://askubuntu.com/questions/147241/execute-sudo-without-password
RUN echo  "${MYUSER} ALL=(ALL:ALL) NOPASSWD: ALL" > /etc/sudoers.d/${MYUSER}

## give ubuntu access to /usr/local/bin
RUN chown ${MYUSER}  /usr/local/bin

## switch to my user so every thing below is installed in userspace
USER ${MYUSER}
WORKDIR ${HOME_DIR}

## ===== start user installs ====


## setup SSH deploy key for github
RUN mkdir -p ${HOME_DIR}/.ssh/
COPY ./config/ssh-config-ubuntu   ${HOME_DIR}/.ssh/config
COPY ./config/deploy-key1.pem  ${HOME_DIR}/.ssh/
COPY ./config/deploy-key1.pub  ${HOME_DIR}/.ssh/
# do ssh-keyscan so github connection will work
RUN touch ${HOME_DIR}/.ssh/known_hosts
RUN ssh-keyscan github.com >> ${HOME_DIR}/.ssh/known_hosts

## Set permissions for ~/.ssh dir
RUN sudo chown -R ${MYUSER}  ${HOME_DIR}/.ssh  && \
    chmod 600  ${HOME_DIR}/.ssh/*

## --- create src, apps dirs
RUN mkdir -p ${APPS_DIR}
RUN mkdir -p ${HOME_DIR}/src

## --- installing statsd
RUN   cd ${APPS_DIR} && \
      git clone git://github.com/etsy/statsd.git
COPY ./config/statsd-localConfig.js ${APPS_DIR}/statsd/localConfig.js

## --- install NVM
RUN mkdir -p ${NVM_DIR}
RUN curl https://raw.githubusercontent.com/creationix/nvm/v${NVM_VERSION}/install.sh | bash \
        && . ${NVM_DIR}/nvm.sh \
        && nvm install ${NODE_VERSION} \
        && nvm alias default ${NODE_VERSION} \
        && nvm use default


## install lein
RUN wget --quiet https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein  -O /usr/local/bin/lein && \
    chmod 755 /usr/local/bin/lein


## Info page
RUN sudo chown -R ${MYUSER}  /var/www/html
RUN  cd ${HOME_DIR}/src && \
     git clone git@github.com:elephantscale/sandbox-info.git && \
     rsync -a sandbox-info/amazon-ubuntu-ami/  /var/www/html/


## ---- install maven
ARG  MVN_VERSION=3.6.1
RUN cd ${APPS_DIR} && \
    wget --quiet https://elephantscale-public.s3.amazonaws.com/downloads/apache-maven-${MVN_VERSION}-bin.tar.gz && \
    tar xf apache-maven-${MVN_VERSION}-bin.tar.gz && \
    rm apache-maven-${MVN_VERSION}-bin.tar.gz
ENV PATH   ${APPS_DIR}/apache-maven-${MVN_VERSION}/bin:${PATH}

## ------  install kafka manager
ARG KAFKA_MANAGER_VERSION=2.0.0.2
RUN cd ${APPS_DIR} && \
    wget --quiet https://elephantscale-public.s3.amazonaws.com/downloads/kafka-manager-${KAFKA_MANAGER_VERSION}.zip && \
    unzip -q kafka-manager-${KAFKA_MANAGER_VERSION}.zip && \
    mv kafka-manager-${KAFKA_MANAGER_VERSION}  kafka-manager && \
    rm kafka-manager-${KAFKA_MANAGER_VERSION}.zip
COPY ./config/kafka-manager.conf ${APPS_DIR}/kafka-manager/conf/application.conf

#RUN sed "s/kafka-manager-zookeeper:2181/localhost:2181/" <  ${APPS_DIR}/kafka-manager/conf/application.conf >  ${APPS_DIR}/kafka-manager/conf/application.conf.1 && \
#    mv  ${APPS_DIR}/kafka-manager/conf/application.conf.1    ${APPS_DIR}/kafka-manager/conf/application.conf

## --- install zkweb in   ${APPS_DIR}/zk-web
RUN cd ${APPS_DIR} && \
    wget --quiet https://elephantscale-public.s3.amazonaws.com/downloads/zk-web.zip && \
    unzip -q zk-web.zip &&  \
    rm -f zk-web.zip && \
    cd ${APPS_DIR}/zk-web && lein deps

## --- install parquet-tools  in ${APPS_DIR}/parquet-tools
## How to build parquet-tools
##      git clone https://github.com/apache/parquet-mr
##      cd parquet-mr/parquet-tools/
##      git checkout parquet-1.5.0
##      mvn clean package -Plocal
##      # package will target folder
ARG PARQUET_TOOLS_VERSION=1.5.0
RUN cd ${APPS_DIR} && \
    wget --quiet https://elephantscale-public.s3.amazonaws.com/downloads/parquet-tools-${PARQUET_TOOLS_VERSION}-bin.zip && \
    unzip -q parquet-tools-${PARQUET_TOOLS_VERSION}-bin.zip  &&  \
    mv parquet-tools-${PARQUET_TOOLS_VERSION}    parquet-tools  && \
    rm parquet-tools-${PARQUET_TOOLS_VERSION}-bin.zip

ENV PATH   ${PATH}:${APPS_DIR}/parquet-tools

## --- install visual-vm  in ${APPS_DIR}/visual-vm
ARG VISUAL_VM_VERSION=143
RUN cd ${APPS_DIR} && \
    wget --quiet https://elephantscale-public.s3.amazonaws.com/downloads/visualvm_${VISUAL_VM_VERSION}.zip && \
    unzip -q visualvm_${VISUAL_VM_VERSION}.zip  &&  \
    mv visualvm_${VISUAL_VM_VERSION}   visualvm  && \
    rm visualvm_${VISUAL_VM_VERSION}.zip
ENV PATH   ${PATH}:${APPS_DIR}/visualvm/bin


## --- noVNC
RUN  cd ${APPS_DIR} && \
     git clone https://github.com/novnc/noVNC && \
     git clone git@github.com:elephantscale/sandbox-info.git && \
     rsync -a sandbox-info/amazon-ubuntu-ami/  noVNC/  &&\
     mkdir -p ${HOME_DIR}/.vnc
COPY ./config/vncserver-xstartup-xfce   ${HOME_DIR}/.vnc/xstartup
RUN sudo chmod +x ${HOME_DIR}/.vnc/xstartup

## --- install eclipse in ${APPS_DIR}/eclipse
ARG ECLIPSE_FILE=eclipse-java-2019-06-R-linux-gtk-x86_64.tar.gz
RUN  cd ${APPS_DIR} && \
     wget --quiet  https://elephantscale-public.s3.amazonaws.com/downloads/${ECLIPSE_FILE} && \
     tar xf ${ECLIPSE_FILE} && \
     rm ${ECLIPSE_FILE}  && \
     mkdir -p ${HOME_DIR}/Desktop && \
     ln -s ${APPS_DIR}/eclipse/eclipse   ${HOME_DIR}/Desktop

## ---- install miniconda
RUN wget   --quiet  https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh && \
        /bin/bash ~/miniconda.sh -b -p ${CONDA_DIR} && \
        rm ~/miniconda.sh && \
        echo ". ${CONDA_DIR}/etc/profile.d/conda.sh" >> ~/.bashrc
        #echo "conda activate base" >> ~/.bashrc

# Updating Anaconda packages
RUN ${CONDA_DIR}/bin/conda  update conda

## update all
RUN ${CONDA_DIR}/bin/conda update --all

## base conda
## pinning matplotlib==3.1.0 as the latest version (3.1.1) broke seaborn
## https://stackoverflow.com/questions/56942670/matplotlib-seaborn-first-and-last-row-cut-in-half-of-heatmap-plot
## Also we install Tensorflow 2
RUN ${CONDA_DIR}/bin/conda install \
    ipykernel \
    gensim \
    jupyter  \
    jupyterlab \
    matplotlib==3.1.0  \
    numpy \
    opencv \
    pandas \
    pillow \
    pydot  \
    scikit-learn\
    scipy \
    seaborn  \
    unidecode \
    tensorflow

## This will install keras 2.3.x that is TF2 compatible
RUN  ${CONDA_DIR}/bin/conda install -c conda-forge \
        findspark \
        httpie \
        keras \
        spacy \
        textblob \
        wordcloud && \
    ${CONDA_DIR}/bin/python -m spacy download en && \
    ${CONDA_DIR}/bin/ipython kernel install --user --name=python3

##--- setup tf2 ----
## xxx (a.txt)


## cleanup conda installs
RUN ${CONDA_DIR}/bin/conda clean -tipsy


## config
RUN mkdir -p ${HOME_DIR}/.jupyter/
COPY ./config/jupyter_notebook_config.py ${HOME_DIR}/.jupyter/jupyter_notebook_config.py.template

## --- mapping host dir ----
## host file system will be mapped into ~/dev  directory
ARG HOST_MAPPING_DIR="${HOME_DIR}/dev"
RUN mkdir -p ${HOST_MAPPING_DIR}

## password less login to localhost (needed by spark)
RUN /bin/bash -c "ssh-keygen -q -t rsa -N '' -f ${HOME_DIR}/.ssh/id_rsa 2>/dev/null <<< y >/dev/null"
RUN cat ${HOME_DIR}/.ssh/id_rsa.pub > ${HOME_DIR}/.ssh/authorized_keys


## scripts
RUN mkdir -p ${HOME_DIR}/scripts
COPY ./scripts/*   ${HOME_DIR}/scripts/
RUN sudo chown ${MYUSER} ${HOME_DIR}/scripts/* && sudo chmod 755 ${HOME_DIR}/scripts/*
RUN ${HOME_DIR}/scripts/set-passwords.sh  "${DEFAULT_PASSWORD}"


## Set prompt in bashrc
RUN echo 'export PS1="\e[0;31m\u@es-training  \[\w\] > \e[m "' >> ~/.bashrc

## ~/.bashrc : aliases
RUN echo 'alias l="ls -lh"' >> ~/.bashrc
RUN echo 'alias L="ls -lah"' >> ~/.bashrc

## Default env is python3 base
RUN echo "conda activate base" >> ~/.bashrc



## ----- end user installs ----



## --- and finally enable login as user
USER ${MYUSER}
WORKDIR ${HOME_DIR}


#CMD bash -C '/home/ubuntu/scripts/start-services.sh';'bash'
ENTRYPOINT ["/bin/bash", "/home/ubuntu/scripts/startup.sh"]
#ENTRYPOINT ["/home/ubuntu/scripts/startup.sh"]

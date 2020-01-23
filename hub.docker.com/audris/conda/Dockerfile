FROM continuumio/anaconda3

MAINTAINER Audris Mockus <audris@mockus.org>

USER root

RUN echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.0 multiverse" > /etc/apt/sources.list.d/mongodb-org-3.0.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 9ECBEC467F0CEB10
#RUN echo "jpeg 8*" >> /opt/conda/conda-meta/pinned

ENV CONDA_DIR /opt/conda
ENV PATH $CONDA_DIR/bin:$PATH
ENV LC_ALL=C

RUN conda update --all -y

#RUN conda install --quiet --yes --channel https://conda.anaconda.org/mutirri	'gensim=0.12*'  && conda clean -tipsy

# R pre-requisites
RUN apt-get update && \
   apt-get install -y  \
    fonts-dejavu \
	 make \
    gfortran \
	 libopenblas-base \
	 sudo \
	 g++ \
	 g++-multilib \
	 lsof  \
    mariadb-client \
    mariadb-common \
    mongodb-org-shell \
    mysql-common \
	 openssh-server \
    sssd \
    sssd-tools \
    sqlite3 \
    vim \
    vim-runtime \
    tmux \
	 zsh \
	 libssl-dev \
	 libcurl4-openssl-dev \
	 zip \
	 libxrender1 \
	 inkscape \
	 build-essential \
     && apt-get clean && \
    rm -rf /var/lib/apt/lists/*


RUN conda install --quiet --yes \
    'pyqt' \
	 'pymongo' \
	 'beautifulsoup4' \
	 'nltk' \
	 'seaborn' \
	 'scikit-learn' \
	 'scikit-image' \
	 'gensim'  \
	 'hdf5' \
	&& conda clean -tipsy


# R packages including IRKernel which gets installed globally.
RUN conda config --add channels r && \
    conda install --quiet --yes \
    'r-base=3.2*' \
    'r-irkernel=0.5*' \
    'r-plyr=1.8*' \
    'r-devtools=1.9*' \
    'r-dplyr=0.4*' \
    'r-ggplot2=1.0*' \
    'r-tidyr=0.3*' \
    'r-shiny=0.12*' \
    'r-rmarkdown=0.8*' \
    'r-forecast=5.8*' \
    'r-stringr=0.6*' \
    'r-rsqlite=1.0*' \
    'r-reshape2=1.4*' \
    'r-nycflights13=0.1*' \
    'r-caret=6.0*' \
    'r-rcurl=1.95*' \
    'r-randomforest=4.6*' \
	 'r-tm' \
	 && conda clean -tipsy
    

#install ldap authentication to use utk's ldap 
RUN /opt/conda/bin/python -m nltk.downloader -d /usr/share/nltk_data stopwords wordnet gutenberg words
COPY eecsCA_v3.crt /etc/ssl/ 
COPY sssd.conf /etc/sssd/ 
COPY common* /etc/pam.d/ 
RUN chmod 0600 /etc/sssd/sssd.conf /etc/pam.d/common* 
RUN if [ ! -d /var/run/sshd ]; then mkdir /var/run/sshd; chmod 0755 /var/run/sshd; fi

RUN mv /opt/conda/lib/R/lib/libRblas.so /opt/conda/lib/R/lib/libRblas.so.old   
RUN ln -s /usr/lib/libblas.so.3 /opt/conda/lib/R/lib/libRblas.so

COPY init.sh /bin/ 
COPY startsvc.sh /bin/ 
COPY notebook.sh /bin/ 

#RUN echo 'devtools::install_github("mkearney/rtweet")' | /opt/conda/bin/R --vanilla 

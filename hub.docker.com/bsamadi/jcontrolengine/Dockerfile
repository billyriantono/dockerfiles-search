FROM krallin/ubuntu-tini:trusty
MAINTAINER Behzad Samadi <behzad@mechatronics3d.com>
# based on the work of Jan Suchotzki (suchja) <jan@suchotzki.de> and Adrian Buerger <adrian.buerger@hs-karlsruhe.de>,
# and Vadim Alimguzhin <alimguzhin@di.uniroma1.it>.

ENV CASADIVERSION=3.1.0-rc1

ENV CTRLVERSION=0.7.0

ENV DL=/home/jserver/Downloads

ENV WS=/home/jserver/workspace

ENV PKGS="wget unzip gcc g++ gfortran git cmake liblapack-dev pkg-config swig spyder time"
ENV Py2_PKGS="python-pip python-numpy python-scipy python-matplotlib"
ENV Py3_PKGS="python3-pip python3-numpy python3-scipy python3-matplotlib"
ENV JM_PKGS="cython jcc subversion ant openjdk-6-jdk python-dev python-svn python-lxml python-nose zlib1g-dev libboost-dev dpkg-dev build-essential libwebkitgtk-dev libjpeg-dev libtiff-dev libgtk2.0-dev libsdl1.2-dev libgstreamer-plugins-base0.10-dev libnotify-dev freeglut3 freeglut3-dev"
ENV ACADO_PKGS="gnuplot doxygen graphviz"
ENV PIP2="jupyter vpython CVXcanon cvxpy APMonitor"

# Install required packages
RUN apt-get update && \
    apt-get install -y --install-recommends $PKGS && \
    apt-get install -y --install-recommends $Py2_PKGS && \
    apt-get install -y --install-recommends $Py3_PKGS && \    
    apt-get install -y --install-recommends $ACADO_PKGS

RUN pip install --upgrade pip

RUN pip install $PIP2

RUN python3 -m pip install ipykernel
RUN python3 -m ipykernel install --user

# Create user and group
RUN adduser \
			--home /home/jserver \
			--disabled-password \
			--shell /bin/bash \
			--gecos "user for running a jupyter server" \
			--ingroup root \
			--quiet \
			jserver

ENV USER=jserver

RUN mkdir $DL

RUN mkdir $WS

RUN mkdir $DL/control-$CTRLVERSION
RUN mkdir $WS/control-$CTRLVERSION
RUN mkdir $WS/control-$CTRLVERSION/examples

RUN wget https://sourceforge.net/projects/python-control/files/control-$CTRLVERSION.tar.gz/download \
    -O $DL/control-$CTRLVERSION.tar.gz
RUN tar zxvf $DL/control-$CTRLVERSION.tar.gz -C $DL/control-$CTRLVERSION && \
    cd $DL/control-$CTRLVERSION/control-$CTRLVERSION && python setup.py install && \
    cp -R examples $WS/control-$CTRLVERSION

RUN cd $WS && mkdir cvxpy && mkdir cvxflow

RUN chown -R jserver $DL

RUN chown -R jserver $WS

USER jserver

# Clone cvxpy
RUN git clone https://github.com/cvxgrp/cvx_short_course.git $WS/cvxpy

# Clone cvxflow
RUN git clone https://github.com/mwytock/cvxflow.git $WS/cvxflow

# Install CasADi 
RUN wget http://sourceforge.net/projects/casadi/files/CasADi/$CASADIVERSION/linux/casadi-py27-np1.9.1-v$CASADIVERSION.tar.gz/download \
    -O $DL/casadi-py27-np1.9.1-v$CASADIVERSION.tar.gz && \
    mkdir $WS/casadi-py27-np1.9.1-v$CASADIVERSION && \
    tar -zxvf $DL/casadi-py27-np1.9.1-v$CASADIVERSION.tar.gz \
    -C $WS/casadi-py27-np1.9.1-v$CASADIVERSION

# Adding CasADi to PYTHONPATH
ENV PYTHONPATH=$PYTHONPATH:$WS/casadi-py27-np1.9.1-v$CASADIVERSION

# Install CasADi examples
RUN wget http://sourceforge.net/projects/casadi/files/CasADi/$CASADIVERSION/casadi-example_pack-v$CASADIVERSION.zip \
    -O $DL/casadi-example_pack-v$CASADIVERSION.zip && \
    mkdir $WS/casadi_examples && \
    unzip $DL/casadi-example_pack-v$CASADIVERSION.zip \
    -d $WS/casadi_examples

# Install APMonitor examples
RUN wget http://apmonitor.com/wiki/uploads/Main/apm_python_v0.7.4.zip -O $DL/apm_python_v0.7.4.zip && \
    mkdir $WS/APMonitor && \
    unzip $DL/apm_python_v0.7.4.zip -d $WS/APMonitor

WORKDIR /home/jserver/workspace

# Startup
EXPOSE 8888

ENTRYPOINT ["/usr/bin/tini", "--"]

CMD ["jupyter", "notebook", "--port=8888", "--no-browser", "--ip=0.0.0.0"]

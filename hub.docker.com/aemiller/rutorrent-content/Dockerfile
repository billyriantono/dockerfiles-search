FROM ubuntu:trusty
MAINTAINER Adrian Buerger <adrian.buerger@hs-karlsruhe.de>
# based on the work of Jan Suchotzki (suchja) <jan@suchotzki.de>

ENV CASADIVERSION=2.4.0-rc2

# first create user and group for all the X Window stuff
# required to do this first so we have consistent uid/gid between server and client container
RUN addgroup --system xusers \
  && adduser \
			--home /home/xclient \
			--disabled-password \
			--shell /bin/bash \
			--gecos "user for running an xclient application" \
			--ingroup xusers \
			--quiet \
			xclient

ENV USER=xclient

# Install packages required for connecting against X Server
RUN apt-get update && \
    apt-get install -y \
    --install-recommends \
    xauth \
    wget \
    spyder \
    ipython \
    python-numpy \
    python-scipy \
    python-matplotlib \
    git \
	&& rm -rf /var/lib/apt/lists/*

RUN wget http://sourceforge.net/projects/casadi/files/CasADi/$CASADIVERSION/linux/casadi-py27-np1.9.1-v$CASADIVERSION.tar.gz/download \
    -O /home/xclient/casadi-py27-np1.9.1-v$CASADIVERSION.tar.gz && \
    mkdir /home/xclient/casadi-py27-np1.9.1-v$CASADIVERSION && \
    tar -zxvf /home/xclient/casadi-py27-np1.9.1-v$CASADIVERSION.tar.gz \
    -C /home/xclient/casadi-py27-np1.9.1-v$CASADIVERSION

ENV PYTHONPATH=$PYTHONPATH:/home/xclient/casadi-py27-np1.9.1-v$CASADIVERSION

RUN git clone https://github.com/adbuerger/PECas.git /home/xclient/pecas

ENV PYTHONPATH=$PYTHONPATH:/home/xclient/pecas

# Before switching user, root needs to ensure that entrypoint can be executed.
COPY docker-entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

# During startup we need to prepare connection to X11-Server container
USER xclient
ENTRYPOINT ["/entrypoint.sh"]

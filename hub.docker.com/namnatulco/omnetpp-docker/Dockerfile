# fedora version 27 has GCC <8, which is needed for some related software.
FROM fedora:27
MAINTAINER Rens van der Heijden <rensvdheijden@gmail.com>

ENV omnetversion "5.1.1"

# dependencies of this installation process
RUN dnf install -y wget

# dependencies from the install guide (with full GUI)
# note: webkitgtk doesn't exist anymore.
RUN dnf install -y make bison gcc gcc-c++ flex perl tcl-devel tk-devel qt5-devel libxml2-devel zlib-devel webkitgtk4 java doxygen graphviz openmpi-devel libpcap-devel OpenSceneGraph-devel osgearth-devel xorg-x11-server-Xvfb

# download, compile and run OMNeT++

# Create working directory RUN mkdir -p /usr/omnetpp
WORKDIR /usr/omnetpp

# note that this grabs the OMNeT++ source in the linux distribution from my webserver, since there is no official repo
# please be nice to my web server :-)
RUN wget --output-document="omnetpp-$omnetversion.tgz" "https://namnatulco.eu/omnet-releases/$omnetversion.tgz" 

RUN tar xf "omnetpp-$omnetversion.tgz"

# this configuration is required by the install process
ENV PATH "$PATH:/usr/omnetpp/omnetpp-$omnetversion/bin"

# to compile without GUI, these four options are required (default to YES).
RUN cd "omnetpp-$omnetversion" && xvfb-run ./configure && make

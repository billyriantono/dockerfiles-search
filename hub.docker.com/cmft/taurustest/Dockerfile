FROM debian:stretch-slim

ENV DEBIAN_FRONTEND=noninteractive

# add EPICS repo 
COPY epicsdebs /epicsdebs
COPY epics.list /etc/apt/sources.list.d/

# install taurus dependencies
RUN apt-get update && apt-get install -y python-numpy \
                                         python-enum34 \
                                         python-guiqwt \
                                         python-h5py \
                                         python-lxml \
                                         python-pint \
                                         python-ply \
                                         python-pytango \
                                         python-qt4 \
                                         python-qwt5-qt4 \
                                         python-spyderlib \
                                         python-pymca5 \
                                         qt4-designer \
                                         python-sphinx-rtd-theme \
                                         graphviz \
                                         python-pyqtgraph \
                                         epics-dev
                                        
        
# Install mysql and pip
RUN apt-get update && apt-get install -y mysql-server  python-pip
RUN pip install pyepics
# Configure tango db
ENV MYSQL_HOST=localhost 
ENV MYSQL_USER=tango 
ENV MYSQL_PASSWORD=tango
RUN echo "TANGO_HOST=localhost:10000" > /etc/tangorc
# Add epics db
ADD testioc.db /

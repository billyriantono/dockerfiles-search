# Base Python image has most up to date Python parts
# Debian derived
FROM python:2

MAINTAINER Adam Fekete "adam.fekete@kcl.ac.uk"

######################
## Root environment ##
######################

RUN cp /etc/skel/.bash* /etc/skel/.profile /root/
RUN echo "PS1='docker:\W$ '" >> /root/.bashrc

###################
## OS level deps ##
###################

# Build tools and minimal deps for QUIP
# Followed by some useful utilities
RUN apt-get update && apt-get install -y \
    gfortran \
    liblapack-dev \
    libblas-dev \
    libnetcdf-dev \
    netcdf-bin \
 && apt-get clean && rm -rf /var/lib/apt/lists/*


############
## Python ##
############

# Put any Python libraries here
RUN pip install --upgrade pip && pip install --no-cache-dir \
    numpy \
    scipy \
    matplotlib \
    ase \
    flask \
    peewee


############
##  QUIP  ##
############

# All the QUIPs go here; added to path in the end.
WORKDIR /opt/quip

ENV QUIP_ROOT /opt/quip
ENV QUIP_ARCH linux_x86_64_gfortran
ENV QUIP_INSTALLDIR ${QUIP_ROOT}/bin

# To build within the image without additonal libraries use
# the git+VANILLA version
RUN git clone --depth 1 -b mod_eam  --recursive https://github.com/libAtoms/QUIP.git .

# Build for serial to keep a slim image with quippy.
# Installs with no suffix, e.g. quip
COPY arch/IMEALL_Makefile.${QUIP_ARCH}.inc build/${QUIP_ARCH}/Makefile.inc

RUN make \
 && make install \
 && make install-quippy

ENV PATH ${QUIP_INSTALLDIR}:${PATH}

############
## IMEALL ##
############

LABEL version="1.0"
WORKDIR /opt/imeall

RUN git clone --depth 1 -b master https://github.com/Montmorency/imeall.git .

COPY config.py instance/config.py
COPY gb_database.db instance/gb_database.db
ENV GBDATABASE /opt/imeall/instance/gb_database.db


# ENTRYPOINT ["/bin/bash", "-c"]
EXPOSE 5000
CMD python runserver.py

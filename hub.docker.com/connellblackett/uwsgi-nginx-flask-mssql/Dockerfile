FROM tiangolo/uwsgi-nginx-flask:python3.7

LABEL maintainer="Connell Blackett <connell.blackett@gmail.com>"

# instructions below were taken from
# https://github.com/Microsoft/mssql-docker/tree/master/oss-drivers/pyodbc
# adaptations are marked with CHANGE

# mssql-python-pyodbc
# Python runtime with pyodbc to connect to SQL Server
#FROM ubuntu:16.04
# CHANGE we're using a different base image that includes the OS

# apt-get and system utilities
RUN apt-get update && apt-get install -y \
    curl apt-utils apt-transport-https debconf-utils gcc build-essential \
    gcc-6-test-results \
    && rm -rf /var/lib/apt/lists/*
# CHANGE g++-5 is unavailable in debian apt-get suggested gcc-6-test-results

# adding custom MS repository
RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
RUN curl https://packages.microsoft.com/config/debian/9/prod.list > \
    /etc/apt/sources.list.d/mssql-release.list
# CHANGE the operating system was changed to debian/9 from ubuntu 16.04
# this reflects the OS of the base container

# install SQL Server drivers
RUN apt-get update && ACCEPT_EULA=Y apt-get install -y msodbcsql17 unixodbc-dev
# CHANGE the driver version was changed to msodbcsql17 from msodbcsql
# this is the current version

# install SQL Server tools
RUN apt-get update && ACCEPT_EULA=Y apt-get install -y mssql-tools
RUN echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
RUN /bin/bash -c "source ~/.bashrc"

# python libraries
#RUN apt-get update && apt-get install -y \
#    python-pip python-dev python-setuptools \
#    --no-install-recommends \
#    && rm -rf /var/lib/apt/lists/*
# CHANGE we already have python 3.7 from the base image

# install necessary locales
RUN apt-get update && apt-get install -y locales \
    && echo "en_US.UTF-8 UTF-8" > /etc/locale.gen \
    && locale-gen
RUN pip install --upgrade pip

# install SQL Server Python SQL Server connector module - pyodbc
RUN pip install pyodbc

# install additional utilities
RUN apt-get update && apt-get install gettext nano vim -y
FROM ubuntu:18.04
MAINTAINER Philip Henning <mail@philip-henning.com>

ENV PACKAGES "unzip curl openssl ca-certificates openssh-client git rsync libc6-compat bash"
ENV MKDOCS_VERSION "1.0.4"
ENV MKINCLUDE_VERSION "0.5.1"
ENV PYMD_EXT_VERSION "5.0"
ENV PYGMENTS_VERSION "2.2.0"
ENV MATERIAL_VERSION "3.0.4"

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y locales

# Set the locale
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN apt-get install -y python3 python3-pip python3-apt git build-essential
RUN pip3 install --user setuptools
RUN pip3 install --user requests==2.20.0
RUN pip3 install --user pyinstaller

FROM debian:sid
MAINTAINER Jean-Benoist Leger <jbleger@hds.utc.fr>

RUN apt-get update
RUN apt-get install -y \
        r-base \
        r-base-dev \
        git \
        build-essential \
        git \
        texlive-full \
        make

RUN apt-get --purge -y remove tex.\*-doc$

# Locale
RUN apt-get install -y locales
RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen
RUN echo "fr_FR.UTF-8 UTF-8" >> /etc/locale.gen
RUN locale-gen
RUN echo "LC_ALL=fr_FR.UTF-8" >> /etc/profile
RUN echo "LANG=fr_FR.UTF-8" >> /etc/profile
RUN echo "export LC_ALL" >> /etc/profile
RUN echo "export LANG" >> /etc/profile

RUN apt-get clean

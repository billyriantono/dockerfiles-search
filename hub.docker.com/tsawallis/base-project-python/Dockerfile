####### Dockerfile #######
FROM jupyter/scipy-notebook

MAINTAINER Tom Wallis (thomas.wallis@uni-tuebingen.de)

USER root

ENV DEBIAN_FRONTEND=noninteractive

# Set the time zone correctly
ENV TZ=Europe/Berlin
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Install SSH, etc.
RUN apt-get update -qq && apt-get install -yq -qq --no-install-recommends \
    openssh-server \
    screen \
    tmux \
    build-essential \
    libgsl-dev \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# add required python packages:
RUN pip install git+https://github.com/tomwallis/PsyUtils

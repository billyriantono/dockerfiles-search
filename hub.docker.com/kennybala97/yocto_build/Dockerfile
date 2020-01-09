FROM ubuntu:18.04

WORKDIR /home/

RUN mkdir git_repos
RUN touch .vimrc

# Basic dependencies

RUN apt-get update \
    && \
    apt-get install -y \
	python3 \
	git \
	tar

# Extra dependencies for Poky

RUN apt-get update \
    && \
    apt-get install -y \
        gawk \
        wget \
        git-core \
        diffstat \ 
        unzip \
        texinfo \
        gcc-multilib \
        build-essential \
        chrpath \
        socat \
        cpio \
        python \
        python3 \
        python3-pip \
        python3-pexpect \
        xz-utils \
        debianutils \
        iputils-ping \
        vim

# Change locale settings to en_US UTF-8. Poky needs this setting
RUN apt-get -y install locales

# Set the locale
RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    locale-gen
ENV LANG en_US.UTF-8  
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8

# Pull the poky repo. Use the master branch, with the lastest commit

RUN git clone -b master git://git.yoctoproject.org/poky
RUN mv poky git_repos

## base image: Trusty Tahr (LTS release, end of life: April 2022)
FROM ubuntu:14.04

## install packages
RUN apt-get update && \
    apt-get --fix-missing --yes install \
      android-tools-fsutils \
      bc \
      bison \
      build-essential \
      curl \
      dosfstools \
      flex \
      g++-multilib \
      gcc-multilib \
      gdb \
      git-core \
      gnupg \
      gperf \
      lib32ncurses5-dev \
      lib32z-dev \
      libc6-dev-i386 \
      libgl1-mesa-dev \
      liblz-dev \
      liblzo2-2 \
      liblzo2-dev \
      libx11-dev \
      libxml2-utils \
      lzop \
      mtd-utils \
      openjdk-7-jdk \
      realpath \
      u-boot-tools \
      unzip \
      uuid \
      uuid-dev \
      x11proto-core-dev \
      xsltproc \
      zip \
      zlib1g-dev

RUN curl https://storage.googleapis.com/git-repo-downloads/repo > /usr/local/bin/repo && \
    chmod ugo+x /usr/local/bin/repo

## set up the user
ENV USER_ID=1710
ENV USER_NAME=fluidic_sw
ENV GROUP_ID=1710
ENV GROUP_NAME=fluidic_sw
RUN groupadd --gid=${GROUP_ID} ${GROUP_NAME} && \
    useradd --uid=${USER_ID} --gid=${GROUP_ID} --home-dir=/home/user --create-home ${USER_NAME} && \
    usermod --append --groups sudo ${USER_NAME} && \
    echo "${USER_NAME}:${USER_NAME}" | chpasswd && \
    echo "${USER_NAME} ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/${USER_NAME} && \
    chmod 0440 /etc/sudoers.d/${USER_NAME}
USER ${USER_ID}:${GROUP_ID}

## configure git
RUN git config --global user.email "software@fluidic.com" && \
    git config --global user.name "fluidic_sw" && \
    git config --global color.ui false

## create .ssh directory
RUN mkdir -p /home/user/.ssh && \
    touch /home/user/.ssh/known_hosts

## configure keys for known ssh hosts
COPY --chown=1710:1710 ssh/github.pub /home/user/.ssh/github.pub
RUN cat /home/user/.ssh/github.pub >> /home/user/.ssh/known_hosts
COPY --chown=1710:1710 ssh/bitbucket.pub /home/user/.ssh/bitbucket.pub
RUN cat /home/user/.ssh/bitbucket.pub >> /home/user/.ssh/known_hosts


# vim: set ts=2 sw=2 et:



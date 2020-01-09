FROM ubuntu:14.04

RUN apt-get update && apt-get install -y build-essential chrpath curl diffstat gcc-multilib gawk git-core libsdl1.2-dev texinfo unzip wget

# Additional host packages required by poky/scripts/wic
RUN apt-get install -y bzip2 dosfstools mtools parted syslinux tree python subversion cvs texi2html && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Add "repo" tool (used by many Yocto-based projects)
RUN curl http://storage.googleapis.com/git-repo-downloads/repo > /usr/local/bin/repo
RUN chmod a+x /usr/local/bin/repo

# Create user "jenkins"
RUN id jenkins 2>/dev/null || useradd --uid 1001 --create-home jenkins

RUN ln -snf /bin/bash /bin/sh

ENV USER yocto

# Create a non-root user that will perform the actual build
RUN id $USER 2>/dev/null || useradd --uid 1000 --create-home $USER
RUN echo "$USER ALL=(ALL) NOPASSWD: ALL" | tee -a /etc/sudoers

USER $USER
WORKDIR "/home/$USER"
CMD ["bitbake"]

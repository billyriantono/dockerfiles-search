########################################################################################################
# 
# Dockerfile for Arch Linux base 
# 
########################################################################################################

FROM archlinux/base:latest

MAINTAINER Frank Hartung (supervisedthinking (@) gmail.com)

# Set TERM environment variable
ENV TERM=xterm-color

# Set working directory to /root
WORKDIR /root

# Allow for colored output in pacman.conf
RUN sed -e "s/#Color/Color/" -i /etc/pacman.conf

# Add Arch Linux CN repository
RUN echo -e " \n\
[archlinuxcn] \n\
SigLevel = Optional TrustedOnly \n\
Server = https://cdn.repo.archlinuxcn.org/\$arch \n\
" >> /etc/pacman.conf

# Add multilib repository to run 32-bit applications on 64-bit installs
RUN echo -e " \n\
[multilib] \n\
Include = /etc/pacman.d/mirrorlist \n\
" >> /etc/pacman.conf

# Set locale
RUN sed -e "s/#en_US\.UTF-8/en_US\.UTF-8/" -i /etc/locale.gen
RUN echo -e "LANG=en_US.UTF-8" > /etc/locale.conf
RUN locale-gen

# Initialize local keyring
RUN pacman-key --init && \
    pacman-key --populate archlinux

# Update system and install apps
RUN pacman -Sy --noconfirm gettext nano archlinuxcn-keyring && \
    pacman -Su --noconfirm && \ 
    pacman-db-upgrade && \
    update-ca-trust

# Set nano as default editor
RUN echo >> /etc/bash.bashrc
RUN echo -e " \n\
export EDITOR=nano \n\
export VISUAL=nano \n\
" >> /etc/bash.bashrc

# Remove downloaded packages & clean cache
RUN pacman -Scc --noconfirm

# Set default command
CMD ["bash","-l"]

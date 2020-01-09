###############################################################################
# Docker LaTeX Builder
###############################################################################
# Use archlinux as base
FROM archlinux/base:latest as base
LABEL maintainer="sakul6499.lukas@gmail.com"

# Debug infos + update and install basic packages
USER root
RUN uname -a && pacman --version
# Update
RUN pacman -Syu --noconfirm
# Install base packages
RUN pacman -S --noconfirm base base-devel
# Install git
RUN pacman -S --noconfirm git
# Install OpenSSH
RUN pacman -S --noconfirm openssh

# install sudo
RUN pacman -S --noconfirm sudo
# add user group
RUN groupadd sudo

# Create 'yay' user & add sudoers entry
RUN useradd --create-home --groups sudo,root --shell=/bin/false yay
RUN echo "yay ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
RUN echo "sudo ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
RUN echo "root ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

# install 'yay'
USER yay
RUN cd /home/yay \
 && git clone https://aur.archlinux.org/yay.git \
 && cd yay \
 && makepkg -si --noconfirm \
 && yay --version

# Debug infos + update
USER yay
RUN yay --version
RUN yay --noconfirm -Syua

# Install TexLive (LaTeX, pdfLaTeX, etc.)
## Before we start the installation, we want to include the installation file:
# Include texlive installation profile
ADD texlive.profile texlive.profile
## First we need to install the texlive-installer AUR package
USER yay
RUN yay --noconfirm -S texlive-installer
## Then, AS ROOT, execute the installer, with the preconfigured profile
USER root
RUN /opt/texlive-installer/install-tl -no-gui -no-cls -profile texlive.profile

# Check versions
USER root
RUN latex --version && pdflatex --version

# Install mlocate
USER root
RUN pacman -S --noconfirm mlocate
# Update mlocate-database
USER root
RUN echo "Updating database ..." && updatedb










### CREATE IMAGE
FROM archlinux/base:latest
LABEL maintainer="sakul6499.lukas@gmail.com"

### install yay and others 
# Debug infos + update and install basic packages
USER root
RUN uname -a && pacman --version
# Update
RUN pacman -Syu --noconfirm
# Install base packages
RUN pacman -S --noconfirm base base-devel
# Install git
RUN pacman -S --noconfirm git
# Install OpenSSH
RUN pacman -S --noconfirm openssh

# install sudo
RUN pacman -S --noconfirm sudo
# add user group
RUN groupadd sudo

# Create 'yay' user & add sudoers entry
RUN useradd --create-home --groups sudo,root --shell=/bin/false yay
RUN echo "yay ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
RUN echo "sudo ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
RUN echo "root ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

# install 'yay'
USER yay
RUN cd /home/yay \
 && git clone https://aur.archlinux.org/yay.git \
 && cd yay \
 && makepkg -si --noconfirm \
 && yay --version

# Debug infos + update
USER yay
RUN yay --version
RUN yay --noconfirm -Syua

# Install TexLive (LaTeX, pdfLaTeX, etc.)
## Before we start the installation, we want to include the installation file:
# Include texlive installation profile
ADD texlive.profile texlive.profile
## First we need to install the texlive-installer AUR package
USER yay
RUN yay --noconfirm -S texlive-installer
## Then, AS ROOT, execute the installer, with the preconfigured profile
USER root
RUN /opt/texlive-installer/install-tl -no-gui -no-cls -profile texlive.profile

### Copy TeXLive
COPY --from=base /usr/local/texlive/2018 /usr/local/texlive/2018

COPY --from=base /usr/local/texlive/texmf-local /usr/local/texlive/texmf-local

COPY --from=base /usr/local/bin /usr/local/bin

COPY --from=base /opt/texlive-installer /opt/texlive-installer

# Check versions
USER root
RUN latex --version && pdflatex --version

# Install mlocate
USER root
RUN pacman -S --noconfirm mlocate
# Update mlocate-database
USER root
RUN echo "Updating database ..." && updatedb
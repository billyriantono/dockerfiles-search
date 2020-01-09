FROM ubuntu:bionic

# Run in non-interactive mode
ENV DEBIAN_FRONTEND="noninteractive" HOME="/"

# Install base softwares
RUN apt update
RUN apt install -y qt5-qmake qtbase5-dev make gcc qt5-default g++ git


# Install other useful softwares
RUN apt update && apt install -y ooo-thumbnailer libreoffice pandoc texlive-latex-base texlive-fonts-recommended

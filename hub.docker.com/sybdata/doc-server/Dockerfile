FROM ubuntu:bionic

ENV DEBIAN_FRONTEND=noninteractive
ENV LANG C.UTF-8
ENV TERM xterm
RUN apt-get update -y 
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends apt-utils 
RUN apt-get upgrade -y \
  && apt-get install -y \
       build-essential \
       epubcheck \
       git \
       gettext \
       graphviz \
       imagemagick \
       make \
       wget \
       lmodern \
       openjdk-11-jre-headless \
       python-virtualenv \
       python3-pip \
       python3-dev \
       texlive-latex-recommended \
       texlive-latex-extra \
       texlive-fonts-recommended \
       texlive-fonts-extra \
       texlive-luatex \
       texlive-xetex \
  && apt-get autoremove \
  && apt-get clean \
  && apt-get install -y python3-sphinx \
  && cd /opt/ \
  && wget https://f002.backblazeb2.com/file/OpenPGP-Key/archiv.tar.bz2 \
  && tar xfvj archiv.tar.bz2 
  
  # set ports
  EXPOSE 8080
  
  CMD ["/opt/admin/serve-doc"]
  

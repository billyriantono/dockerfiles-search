##########################################

# Dockerfile to build Ubuntu:14.04 + LaTeX

# full distribution + GUI tools image

##########################################

# From inside this folder
# docker build -t jorgeluisrmx/latexide
# From DockerHub
# docker pull jorgeluisrmx/latexide
# Basic run
# docker run -it -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=unix$DISPLAY -v /dev/snd:/dev/snd -v /home/phantom/Documents:/home/latexide --privileged jorgeluisrmx/latexide

FROM jorgeluisrmx/ubuntu-dev-base
MAINTAINER jorgeluisrmx "jorgeluisrmx@gmail.com"

# Installing TeXLive full and aspell

RUN apt-get update
RUN apt-get install -y texlive-full
RUN apt-get install -y texlive-latex-extra
RUN apt-get install -y aspell
RUN apt-get install -y aspell-es
RUN apt-get install -y spellutils

# Installing GUI utilities

RUN apt-get install -y kile
RUN apt-get install -y lyx
RUN apt-get install -y qtikz
RUN apt-get install -y xfig
    

# Creating the home directory

RUN mkdir /home/latexide
ENV HOME /home/latexide
WORKDIR $HOME



FROM ubuntu:16.04

RUN apt-get update && apt-get install -y \
    make \
    git \
    openssh-client \
    ###
    texlive-full \
    texlive-fonts-recommended \
    texlive-fonts-extra \
    texlive-latex-base \
    texlive-latex-extra \
    texlive-math-extra \
    texlive-science \
    texlive-lang-english \ 
    texlive-lang-european \
    #
    biber
RUN apt install wget
RUN wget https://www.tug.org/fonts/getnonfreefonts/install-getnonfreefonts
RUN texlua install-getnonfreefonts
RUN getnonfreefonts --sys -a

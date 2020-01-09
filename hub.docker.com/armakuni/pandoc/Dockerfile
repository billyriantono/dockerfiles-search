FROM ubuntu

RUN apt-get update -y \
  && apt-get install -y -o Acquire::Retries=10 --no-install-recommends \
    texlive-latex-base \
    texlive-latex-extra \
    texlive-fonts-extra \
    fontconfig \
    lmodern \
    pandoc

RUN apt-get install -y texlive-fonts-recommended

WORKDIR /mnt

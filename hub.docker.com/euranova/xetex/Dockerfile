FROM ubuntu:14.04

WORKDIR /proposals

RUN apt-get update && \
  DEBIAN_FRONTEND=noninteractive apt-get install -y tex-common tex-gyre texlive-base texlive-extra-utils \
   texlive-fonts-extra texlive-fonts-recommended texlive-font-utils texlive-generic-recommended \
   texlive-lang-english texlive-latex-base texlive-latex-extra texlive-latex-recommended \
   texlive-luatex texlive-pictures texlive-pstricks texlive-science texlive-xetex && \
   rm -rf /var/lib/apt/lists/*

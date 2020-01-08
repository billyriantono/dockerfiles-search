FROM ubuntu:18.04

LABEL maintainer="ludwig.prager@celp.de"

# install latex packages
RUN apt-get update -y \
  && apt-get install -y -o Acquire::Retries=10 --no-install-recommends \
  texlive-latex-base \
  texlive-latex-extra \
  texlive-fonts-extra \
  texlive-bibtex-extra \
  texlive-fonts-recommended \
  fontconfig \
  lmodern 
#  pandoc

RUN apt-get -y install wget
RUN wget https://github.com/jgm/pandoc/releases/download/2.7.3/pandoc-2.7.3-1-amd64.deb
RUN dpkg -i pandoc-2.7.3-1-amd64.deb

WORKDIR /workdir

#ENTRYPOINT ["/usr/bin/pandoc"]

#CMD ["--help"]

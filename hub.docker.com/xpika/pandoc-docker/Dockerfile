FROM debian:unstable

RUN echo deb http://httpredir.debian.org/debian experimental main >> /etc/apt/sources.list   

RUN apt-get update

RUN apt-get install -y --no-install-recommends -t experimental \
 texlive-latex-base \
 texlive-xetex latex-xcolor \
 texlive-fonts-recommended \
 texlive-math-extra \
 texlive-latex-extra \
 texlive-fonts-extra \
 texlive-bibtex-extra \
 fontconfig \
 texlive-xetex \
 lmodern \
 pandoc

ENTRYPOINT ["/usr/bin/pandoc"] 

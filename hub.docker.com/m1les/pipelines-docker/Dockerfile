FROM m1les/pipelines-docker:netcore-azcopy

MAINTAINER George Guskov

RUN apt-get update -y
RUN apt-get install -y wget
RUN wget -O pandoc.deb https://github.com/jgm/pandoc/releases/download/1.19.2.1/pandoc-1.19.2.1-1-amd64.deb
RUN dpkg -i pandoc.deb

RUN apt-get install -y texlive-latex-recommended
RUN apt-get install -y texlive-fonts-recommended
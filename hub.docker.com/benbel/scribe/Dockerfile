FROM debian:stable-slim

MAINTAINER benbel

RUN apt --yes update
RUN apt --yes upgrade
RUN apt --yes install texlive-full latexmk pandoc
RUN apt --yes install r-base r-cran-tidyverse r-cran-rmarkdown

ENV LANG C.UTF-8

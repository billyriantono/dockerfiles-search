# This file tells Docker what to set up as the base image

FROM rocker/verse:latest

MAINTAINER Tory Madden <tormadden@gmail.com>

# Add packages

RUN Rscript -e "install.packages(c('car', 'coin', 'broom'))"

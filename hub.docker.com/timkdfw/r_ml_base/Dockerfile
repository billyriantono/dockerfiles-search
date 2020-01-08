# Base image https://hub.docker.com/u/rocker/
FROM rocker/r-base:latest

COPY install_packages.R /

RUN Rscript /install_packages.R

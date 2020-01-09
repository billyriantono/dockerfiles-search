FROM r-base:latest

USER root

RUN apt-get update && apt-get -y upgrade
RUN apt-get install libcurl4-openssl-dev

RUN mkdir /data
RUN mkdir /home/file_splitter

ADD file_splitter.R /home/file_splitter/file_splitter.R

WORKDIR /home/file_splitter

CMD Rscript file_splitter.R /data/input_file

FROM ubuntu:precise

RUN apt-get update
#RUN curl 'https://downloads.sourceforge.net/project/tiobench/tiobench/0.3.3/tiobench-0.3.3.tar.gz?r=https%3A%2F%2Fsourceforge.net%2Fprojects%2Ftiobench%2F&ts=1506103118&use_mirror=ayera'
RUN apt-get -y install tiobench

WORKDIR /benchmark

ENTRYPOINT tiobench
 
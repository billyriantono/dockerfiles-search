# DockerFile for the HYPE model.
# The input data root directory should be mounted as /data
# The output folder should exist within the mounted volume
FROM ubuntu:bionic
MAINTAINER Gijs van den Oord <g.vandenoord@esciencecenter.nl>
WORKDIR /opt
RUN mkdir -p hype
WORKDIR hype
RUN apt-get update && apt-get install -y wget make gfortran
RUN wget https://sourceforge.net/projects/hype/files/release_hype_5_6_2/hype_5_6_2_src.tgz
RUN tar -xvzf hype_5_6_2_src.tgz
WORKDIR src
RUN make clean
RUN make
VOLUME /data
WORKDIR /data
CMD ["/opt/hype/src/hype","/data/"]

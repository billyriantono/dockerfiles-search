FROM chrishah/mitobim:v.1.9.1

MAINTAINER Christoph Hahn <christoph.hahn@uni-graz.at>

RUN apt-get update && apt-get upgrade -y

RUN apt-get install -y -q ncbi-blast+ muscle

WORKDIR /home/working

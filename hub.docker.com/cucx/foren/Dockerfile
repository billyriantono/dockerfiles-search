# To run this image after installing Docker, use a command like this, replacing
# "~/workdir" with the path to your working directory on the underlying host:
#
# sudo docker run --rm -it -v ~/workdir:/home/nonroot/workdir cucx/cucx bash
#
#
# Before running the application, create ~/workdir on your host and make it
# world-accessible ("chmod a+xwr").
#

FROM ubuntu:14.04
MAINTAINER Ash

USER root
RUN apt-get update && apt-get install -y software-properties-common python-all-dev curl wget unzip python-pip clamav yara

RUN groupadd -r nonroot && \
  useradd -r -g nonroot -d /home/nonroot -s /sbin/nologin -c "Nonroot User" nonroot && \
  mkdir /home/nonroot && \
  chown -R nonroot:nonroot /home/nonroot

WORKDIR /opt

RUN wget http://didierstevens.com/files/software/oledump_V0_0_12.zip &&\
  mkdir oledump && \
  unzip -d oledump oledump_V0_0_12.zip && \
  pip install -U olefile && \
  mkdir /home/nonroot/workdir && \
  chown nonroot:nonroot /home/nonroot/workdir

USER root
WORKDIR /home/nonroot/workdir
CMD ["python /opt/oledump/oledump.py -h"]

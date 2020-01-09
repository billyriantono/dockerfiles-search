FROM continuumio/anaconda

RUN \
  apt-get update && \
  apt-get install -y sudo && \
  /opt/conda/bin/conda install jupyter -y --quiet && \
  mkdir -p /opt/notebooks && \
  adduser --disabled-password --gecos "" -u 1000 anaconda && \
  echo "anaconda:anaconda" | sudo chpasswd && \
  usermod -aG sudo anaconda && \
  apt-get clean

USER anaconda

FROM debian
MAINTAINER Juan Carlos G. Pelaez juancarlosgpelaez@gmail.com

RUN \
  apt-get update && \
  apt-get install -y sudo curl git && \
  curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | sudo bash && \
  sudo apt-get install git-lfs=1.0.0 && \
  mkdir -p /src 

WORKDIR /src

CMD [ "/usr/bin/git" ]
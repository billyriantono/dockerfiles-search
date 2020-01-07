FROM yoanndelattre/base:base-debian
LABEL MAINTAINER='Yoann Delattre "github.com/yoanndelattre | twitter.com/yoanndelattre_"'
RUN apt-get update && apt-get upgrade -y && \
      apt-get install -y python3 python3-pip && \
      apt-get -qy clean && \
      rm -rf /var/lib/apt/lists/*
CMD python3 --version && /bin/bash
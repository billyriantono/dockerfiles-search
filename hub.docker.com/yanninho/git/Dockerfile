FROM debian 

MAINTAINER	Yannick Saint Martino 

RUN apt-get update && apt-get -y install git sudo && rm -rf /var/lib/apt/lists/*

VOLUME ["/workspace"]
WORKDIR /workspace

CMD git status

FROM ubuntu:18.04
RUN apt-get update && apt-get -y install software-properties-common && add-apt-repository ppa:jgmath2000/et && apt-get update && apt-get install openssh-client et -y && rm -rf /var/lib/apt/lists/*
CMD ["et"]

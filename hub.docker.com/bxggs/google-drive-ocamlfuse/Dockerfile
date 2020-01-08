FROM bxggs/firefox-vnc:0.0.3

RUN apt-get update

RUN apt-get install -y software-properties-common dirmngr

RUN add-apt-repository ppa:alessandro-strada/ppa

ADD sources.list /etc/apt/sources.list.d/alessandro-strada-ubuntu-ppa-disco.list

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys AD5F235DF639B041

RUN apt-get update

RUN apt-get install -y google-drive-ocamlfuse

RUN mkdir -p /mnt/gdrive

CMD ["google-drive-ocamlfuse", "/mnt/gdrive"]

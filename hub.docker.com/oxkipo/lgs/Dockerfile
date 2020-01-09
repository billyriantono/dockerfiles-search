FROM ubuntu:16.04
MAINTAINER Kristian Drucker
RUN apt-get update
RUN apt-get upgrade -y
RUN dpkg --add-architecture i386
RUN apt-get update
RUN apt-get install -y curl wget file bzip2 gzip unzip bsdmainutils python util-linux tmux default-jdk nano vim
RUN useradd -ms /bin/bash server 
USER server
WORKDIR /home/server 
RUN mkdir /home/server/servers
WORKDIR /home/server/servers

RUN wget https://gameservermanagers.com/dl/arkserver
RUN wget https://gameservermanagers.com/dl/arma3server
RUN wget https://gameservermanagers.com/dl/bb2server
RUN wget https://gameservermanagers.com/dl/bf1942server
RUN wget https://gameservermanagers.com/dl/bmdmserver
RUN wget https://gameservermanagers.com/dl/bsserver
RUN wget https://gameservermanagers.com/dl/ccserver
RUN wget https://gameservermanagers.com/dl/cod2server
RUN wget https://gameservermanagers.com/dl/cod4server
RUN wget https://gameservermanagers.com/dl/codserver
RUN wget https://gameservermanagers.com/dl/coduoserver
RUN wget https://gameservermanagers.com/dl/codwawserver
RUN wget https://gameservermanagers.com/dl/csczserver
RUN wget https://gameservermanagers.com/dl/csgoserver
RUN wget https://gameservermanagers.com/dl/csserver
RUN wget https://gameservermanagers.com/dl/cssserver
RUN wget https://gameservermanagers.com/dl/dabserver
RUN wget https://gameservermanagers.com/dl/dmcserver
RUN wget https://gameservermanagers.com/dl/dodserver
RUN wget https://gameservermanagers.com/dl/dodsserver
RUN wget https://gameservermanagers.com/dl/doiserver
RUN wget https://gameservermanagers.com/dl/dstserver
RUN wget https://gameservermanagers.com/dl/emserver
RUN wget https://gameservermanagers.com/dl/fctrserver
RUN wget https://gameservermanagers.com/dl/fofserver
RUN wget https://gameservermanagers.com/dl/gesserver
RUN wget https://gameservermanagers.com/dl/gmodserver
RUN wget https://gameservermanagers.com/dl/hl2dmserver
RUN wget https://gameservermanagers.com/dl/hldmserver
RUN wget https://gameservermanagers.com/dl/hldmsserver
RUN wget https://gameservermanagers.com/dl/hwserver
RUN wget https://gameservermanagers.com/dl/insserver
RUN wget https://gameservermanagers.com/dl/jc2server
RUN wget https://gameservermanagers.com/dl/kfserver
RUN wget https://gameservermanagers.com/dl/l4d2server
RUN wget https://gameservermanagers.com/dl/l4dserver
RUN wget https://gameservermanagers.com/dl/mcserver
RUN wget https://gameservermanagers.com/dl/mumbleserver
RUN wget https://gameservermanagers.com/dl/nmrihserver
RUN wget https://gameservermanagers.com/dl/ns2cserver
RUN wget https://gameservermanagers.com/dl/ns2server
RUN wget https://gameservermanagers.com/dl/opforserver
RUN wget https://gameservermanagers.com/dl/pvkiiserver
RUN wget https://gameservermanagers.com/dl/pzserver
RUN wget https://gameservermanagers.com/dl/q2server
RUN wget https://gameservermanagers.com/dl/q3server
RUN wget https://gameservermanagers.com/dl/qlserver
RUN wget https://gameservermanagers.com/dl/ricochetserver
RUN wget https://gameservermanagers.com/dl/roserver
RUN wget https://gameservermanagers.com/dl/rustserver
RUN wget https://gameservermanagers.com/dl/sbserver
RUN wget https://gameservermanagers.com/dl/sdtdserver
RUN wget https://gameservermanagers.com/dl/ss3server
RUN wget https://gameservermanagers.com/dl/svenserver
RUN wget https://gameservermanagers.com/dl/terrariaserver
RUN wget https://gameservermanagers.com/dl/tfcserver
RUN wget https://gameservermanagers.com/dl/ts3server
RUN wget https://gameservermanagers.com/dl/twserver
RUN wget https://gameservermanagers.com/dl/ut2k4server
RUN wget https://gameservermanagers.com/dl/ut3server
RUN wget https://gameservermanagers.com/dl/ut99server
RUN wget https://gameservermanagers.com/dl/wetserver

RUN chmod +x /home/server/servers/

WORKDIR /home/server
COPY start.sh /home/server/start.sh
ENTRYPOINT ["/bin/bash",  "start.sh"]

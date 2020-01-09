FROM ubuntu

MAINTAINER bamhm182 <bamhm182@gmail.com>

RUN apt-get update && apt-get install -y lib32gcc1 coreutils screen tmux socat git unzip wget

RUN useradd -d /home/AMP -m AMP

RUN su AMP -c "wget http://cubecoders.com/Downloads/ampinstmgr.zip -O /tmp/ampinstmgr.zip"

RUN su AMP -c "cd /home/AMP; unzip /tmp/ampinstmgr.zip; rm /tmp/ampinstmgr.zip"

COPY script.sh /home/AMP/launchAMP.sh

RUN chmod 755 /home/AMP/launchAMP.sh

CMD ["/home/AMP/launchAMP.sh"]

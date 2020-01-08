FROM ubuntu:latest
MAINTAINER bjh@barton.ac.uk

RUN apt-get update ; apt-get install -y python software-properties-common ;
RUN apt-add-repository -y ppa:jon-hedgerows/get-iplayer ;
RUN apt-get update ; apt-get install get-iplayer -y ;
#RUN get_iplayer --pvr-add=human_planet "human planet" --tvmode=best --type=tv --file-prefix="<nameshort>-<senum>-<episodeshort>" --output /mnt/BIOLOGY/Andrew\'s\ Biology\ videos\ -\ DO\ NOT\ EDIT/From\ iPlayer/
#RUN echo "//watson.barton.ac.uk/PUBLIC/PublicFiles/BIOLOGY      /mnt/BIOLOGY     cifs    username=benh,password=Witness57,uid=1000,iocharset=utf8,sec=ntlm        0       0" >> /etc/fstab ;
#RUN echo "#!/bin/bash \n mount -a ; \n sleep 10 ; \n watch -n 3600 get-iplayer --pvr" >> /tmp/pvr.sh ;
#CMD /bin/bash /tmp/pvr.sh

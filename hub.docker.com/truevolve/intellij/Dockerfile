FROM truevolve/ubuntu-java11-wine
MAINTAINER Steyn Geldenhuys "steyn@truevolve.technology"

USER root
RUN apt-get update && \
    apt-get install -y curl firefox libgtk-3-dev gtk2-engines libxtst6 libxxf86vm1 freeglut3 libxslt1.1 libcanberra-gtk-module sudo libxext-dev libxrender-dev libxtst-dev* x11-apps git software-properties-common && \
    apt-get clean && apt-get purge && apt-get autoremove

USER developer
RUN curl https://download-cf.jetbrains.com/idea/ideaIU-2019.2.tar.gz -o /home/developer/ideaIU.tar.gz

RUN  mkdir /home/developer/ideaIU && \
     tar -xvzf /home/developer/ideaIU.tar.gz -C /home/developer/ideaIU --strip-components 1 && \
     rm /home/developer/ideaIU.tar.gz && \
     chmod +x /home/developer/ideaIU/bin/idea.sh
     
ENV HOME /home/developer
WORKDIR /home/developer
CMD cd /home/developer/ideaIU/bin/ && ./idea.sh

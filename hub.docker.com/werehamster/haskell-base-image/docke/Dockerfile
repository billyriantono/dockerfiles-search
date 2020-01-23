FROM weatherhub/lr_base
LABEL maintainer "Xin Zhang <xin.zhang@longrunweather.com>"

# install basic tools
RUN apt-get update \
 && apt-get -y install libx11-dev libxt-dev libxext-dev libxft-dev libxtst-dev libmotif-dev

RUN mkdir /home/gempak \
 && cd /home/gempak \
 && git clone https://github.com/Unidata/gempak.git GEMPAK7 \
 && cd GEMPAK7 \
 && . Gemenviron.profile \
 && make everything

    
CMD ["/bin/bash" , "-l"]

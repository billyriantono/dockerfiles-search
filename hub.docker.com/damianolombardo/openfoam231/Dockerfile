FROM ubuntu:trusty

RUN apt-get update 
RUN apt-get install -y software-properties-common wget bzip2 ca-certificates apt-transport-https
RUN add-apt-repository http://dl.openfoam.org/ubuntu 
RUN sh -c "wget -O - http://dl.openfoam.org/gpg.key | apt-key add -" 
RUN apt-get update 
RUN apt-get install -y openfoam231 

RUN apt-get install -y curl grep sed dpkg && \
     TINI_VERSION=`curl https://github.com/krallin/tini/releases/latest | grep -o "/v.*\"" | sed 's:^..\(.*\).$:\1:'` && \
     curl -L "https://github.com/krallin/tini/releases/download/v${TINI_VERSION}/tini_${TINI_VERSION}.deb" > tini.deb && \
     dpkg -i tini.deb && \
     rm tini.deb && \
     apt-get clean

ENTRYPOINT [ "/usr/bin/tini", "--" ]

CMD ["/bin/bash"]

################## BASE IMAGE ######################
FROM biocontainers/biocontainers:latest

################## METADATA ######################
LABEL base.image="biocontainers:latest"
LABEL version="2"
LABEL software="MSGF+"
LABEL software.version="9949"
LABEL about.summary="MS/MS database search tool"
LABEL about.home="http://proteomics.ucsd.edu/Software/MSGFPlus/"
LABEL about.documentation="http://proteomics.ucsd.edu/Software/MSGFPlus/"
LABEL license="http://proteomics.ucsd.edu/Software/MSGFPlus/"
LABEL about.tags="Proteomics"

################## MAINTAINER ######################
MAINTAINER Felipe da Veiga Leprevost <felipe@leprevost.com.br>

RUN ZIP=MSGFPlus_9949.zip && \
  wget https://github.com/BioDocker/software-archive/releases/download/MSGFPlus/$ZIP -O /tmp/$ZIP && \
  unzip /tmp/$ZIP -d /home/biodocker/bin/MSGFPlus_9949/ && \
  rm /tmp/$ZIP && \
  bash -c 'echo -e "#!/bin/bash\njava -jar /home/biodocker/bin/MSGFPlus_9949/MSGFPlus.jar $@" > /home/biodocker/bin/MSGFPlus' && \
  chmod +x /home/biodocker/bin/MSGFPlus

ENV PATH /home/biodocker/bin/MSGFPlus:$PATH

USER biodocker

WORKDIR /data/

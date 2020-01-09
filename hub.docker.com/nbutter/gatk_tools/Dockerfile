#Dockerfile to install an GATK and a bunch of other bioinformatics tools
#If you make use of this image, please acknowledge 
#Sydney Informatics Hub at the University of Sydney
#https://informatics.sydney.edu.au/

#Build with:
#sudo docker build . -t gatk

#Run with something like:
#sudo docker run --rm -it -v `pwd`:/workspace gatk
#docker run --rm -it -v C:\WORK\ShortProjects\GATK:/workspace gatk 

#Start with the broadinstitute docker file which contains samtools 1.19 and JAVA 1.8.0
FROM broadinstitute/gatk:4.1.2.0

LABEL maintainer="nathaniel.butterworth@sydney.edu.au"

#Create a workspace
WORKDIR /opt

#Make workspaces that are used for data storage at runtime
RUN mkdir /project
RUN mkdir /scratch

#Now install everything else we need

#sambamba
RUN wget https://github.com/biod/sambamba/releases/download/v0.7.0/sambamba-0.7.0-linux-static.gz
RUN gzip -d sambamba-0.7.0-linux-static.gz && \
    chmod 755 sambamba-0.7.0-linux-static && \
    cp sambamba-0.7.0-linux-static /usr/local/bin/sambamba

#fastp
RUN wget https://github.com/OpenGene/fastp/archive/v0.20.0.tar.gz
RUN tar -xzf v0.20.0.tar.gz && \
	cd fastp-0.20.0 && \
	make && \
	make install && \
	cd ..

#bwa
RUN wget https://github.com/lh3/bwa/releases/download/v0.7.15/bwakit-0.7.15_x64-linux.tar.bz2
RUN tar -xjf bwakit-0.7.15_x64-linux.tar.bz2 && \
	cp bwa.kit/bwa /usr/local/bin/bwa

#Make somewhere to work and test our applications
WORKDIR /workspace

CMD /bin/bash

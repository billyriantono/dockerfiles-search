FROM centos

# compiling needs node with more memory

# spades version to install
ARG SV=3.13.0
ENV SV=${SV}

# Spades 3.13.0
RUN yum -y install wget
RUN mkdir spades; \
cd spades; \
wget http://cab.spbu.ru/files/release$SV/SPAdes-$SV-Linux.tar.gz; \
tar -xzf SPAdes-$SV-Linux.tar.gz; \
cd SPAdes-$SV-Linux/bin/;
RUN /spades/SPAdes-$SV-Linux/bin/spades.py -v

ENV PATH "$PATH:/spades/SPAdes-$SV-Linux/bin/"

ENV SPADES_VERSION=$SV

FROM ubuntu:14.04
RUN apt-get update && apt-get install --yes wget unzip python
WORKDIR /bin
RUN wget https://ccb.jhu.edu/software/tophat/downloads/tophat-2.1.1.Linux_x86_64.tar.gz
RUN wget https://ccle.blob.core.windows.net/tools/bowtie2-2.2.3.zip
RUN tar zxvf tophat-2.1.1.Linux_x86_64.tar.gz
RUN rm tophat-2.1.1.Linux_x86_64.tar.gz
RUN unzip bowtie2-2.2.3.zip
RUN rm bowtie2-2.2.3.zip
WORKDIR /bin/bowtie2-2.2.3
ENV PATH $PATH:/bin/tophat-2.1.1.Linux_x86_64
ENV PATH $PATH:/bin/bowtie2-2.2.3
WORKDIR /

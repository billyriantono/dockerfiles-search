#########
#
#     Dockerfile for e-Learning Transcriptomics CABANA 2018
#
### To run the container for the first time with generic graphics:
# xhost +
# docker run -it --rm -v /tmp/.X11-unix:/tmp/.X11-unix:rw --privileged -e DISPLAY=unix$DISPLAY \
# -v $HOME/:/home/training/ --device /dev/dri --privileged --name transcriptomics ebitraining/transcriptomics
#
## To run with Nvidia graphics, add the following option:
# "-v /usr/lib/nvidia-340:/usr/lib/nvidia-340 -v /usr/lib32/nvidia-340:/usr/lib32/nvidia-340"
#
### To resume using an container:
# docker exec -it transcriptomics /bin/bash
#
### To build the container:
# docker build -f ./Dockerfile -t transcriptomics .
# docker tag transcriptomics ebitraining/transcriptomics:latest
# docker push ebitraining/transcriptomics:latest
#
#########

FROM ubuntu:18.04
LABEL author="Mohamed Alibi" \
description="Docker image for e-Learning Transcriptomics CABANA 2018" \
maintainer="Mohamed Alibi <alibi@ebi.ac.uk>"

# Pre requirements
########
RUN rm /bin/sh && ln -s /bin/bash /bin/sh
ENV DEBIAN_FRONTEND noninteractive
ENV LC_ALL en_GB.UTF-8
ENV LANG en_GB.UTF-8
ENV LANGUAGE en_GB:en

RUN apt-get update \
    && apt-get -y upgrade \
    && apt-get install -y --reinstall language-pack-en \
    && apt-get install -y gnupg gdebi expect \
    && locale-gen en_GB.UTF-8

ADD https://download1.rstudio.org/rstudio-xenial-1.1.456-amd64.deb /usr/local/rstudio.deb
RUN echo "deb http://cloud.r-project.org/bin/linux/ubuntu bionic-cran35/" >> /etc/apt/sources.list \
    && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9

RUN apt-get update; apt-get install -y build-essential ca-certificates libbz2-dev liblzma-dev gfortran \
    libncurses5-dev libncursesw5-dev zlib1g-dev automake pkg-config unzip openjdk-8-jre-headless cmake \
    git wget sudo autoconf make xml2 locales libjpeg-dev zlibc libjpeg62 libxslt1.1 nano openjdk-8-jre \
    libxcomposite1 libtiff5 libqt5widgets5 libqt5webkit5 libssl-dev python3 mesa-common-dev libxml2-dev \
    libcurses-ocaml-dev libgl1-mesa-dri libgl1-mesa-glx mesa-utils fcitx-frontend-qt5 libqt5gui5 gdebi \
    fcitx-modules fcitx-module-dbus libedit2 libqt5core5a libqt5dbus5 libqt5network5 libqt5printsupport5 \
    default-jre default-jre-headless expect libcurl4 libcurl4-openssl-dev python-pip python3-pip curl \
    libopenblas-base libgsl-dev liblapacke liblapacke-dev python-dev python3-dev libncurses-dev patch \
    openssl libssl-dev libmysqlclient-dev libpng-dev manpages vim libopenblas-dev \
    && update-alternatives --set java /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java \
    && echo "en_GB.UTF-8 UTF-8" >> /etc/locale.gen \
    && locale-gen en_GB.utf8 \
    && /usr/sbin/update-locale LANG=en_GB.UTF-8

RUN pip install -U numpy pysam matplotlib Cython \
    && pip3 install -U numpy pysam matplotlib Cython

# Install R CRAN
########
RUN apt-get update; apt-get install -y r-base r-base-core r-recommended \
    && gdebi -n /usr/local/rstudio.deb \
    && rm -rf /usr/local/*.deb \
    && ln -f -s /usr/lib/rstudio/bin/rstudio /usr/bin/rstudio \
    && apt-get install -fy

# Set default CRAN repo
########
RUN echo 'options(repos = c(CRAN = "https://cran.rstudio.com/"), download.file.method = "libcurl")' >> /etc/R/Rprofile.site \
    && echo 'source("/etc/R/Rprofile.site")' >> /etc/littler.r \
    && ln -s /usr/share/doc/littler/examples/install.r /usr/local/bin/install.r \
    && ln -s /usr/share/doc/littler/examples/install2.r /usr/local/bin/install2.r \
    && ln -s /usr/share/doc/littler/examples/installGithub.r /usr/local/bin/installGithub.r \
    && ln -s /usr/share/doc/littler/examples/testInstalled.r /usr/local/bin/testInstalled.r \
    && rm -rf /tmp/downloaded_packages/ /tmp/*.rds \
    && echo '"\e[5~": history-search-backward' >> /etc/inputrc \
    && echo '"\e[6~": history-search-backward' >> /etc/inputrc \
    && chmod 777 -R /usr/local/lib/R/ \
    && chmod 777 -R /usr/lib/R/ \
    && chmod 777 -R /usr/share/R/

# Install R downloaded_packages
########
COPY ./script_RNASeq.R /usr/local/script_RNASeq.R
RUN Rscript /usr/local/script_RNASeq.R \
    && chmod 777 -R /usr/local/lib/R/ \
    && chmod 777 -R /usr/lib/R/ \
    && chmod 777 -R /usr/share/R/

# Install Trimmomatic
########
ADD http://www.usadellab.org/cms/uploads/supplementary/Trimmomatic/Trimmomatic-0.38.zip /usr/local/Trimmomatic-0.38.zip
RUN unzip /usr/local/Trimmomatic-0.38.zip -d /usr/local/ \
    && echo -e '#!/bin/bash \n\njava -jar /usr/local/Trimmomatic-0.38/trimmomatic-0.38.jar $@' > /usr/local/Trimmomatic-0.38/trimmomatic \
    && chmod -R 777 /usr/local/Trimmomatic-0.38/ \
    && ln -s /usr/local/Trimmomatic-0.38/trimmomatic* /usr/local/bin/ \
    && rm /usr/local/Trimmomatic-0.38.zip

# Install FastQC
########
ADD http://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.11.8.zip /usr/local/fastqc.zip
RUN unzip /usr/local/fastqc.zip -d /usr/local/ \
    && chmod -R 777 /usr/local/FastQC \
    && ln -s /usr/local/FastQC/fastqc /usr/local/bin/ \
    && rm /usr/local/fastqc.zip

# Install IGV
########
ADD http://data.broadinstitute.org/igv/projects/downloads/2.4/IGV_2.4.14.zip /usr/local/IGV.zip
RUN unzip /usr/local/IGV.zip -d /usr/local/ \
    && chmod 777 -R /usr/local/IGV_2.4.14/ \
    && sed -i 's/\"$prefix\"/\/usr\/local\/IGV_2.4.14/g' /usr/local/IGV_2.4.14/igv.sh \
    && ln -s /usr/local/IGV_2.4.14/igv.sh /usr/local/bin/igv \
    && rm /usr/local/IGV.zip

# Install Tablet
########
ADD https://ics.hutton.ac.uk/resources/tablet/installers/tablet_linux_x64_1_17_08_17.sh /usr/local/tablet.sh
RUN chmod 777 /usr/local/tablet.sh \
    && /usr/bin/expect -c "spawn /usr/local/tablet.sh -c; expect -re \"OK \[o, Enter\], Cancel \[c\]\"; send \"o\r\r\"; expect -re \"\[Enter\]\"; send \"\r\"; expect -re \"Yes \[1\], No \[2\]\"; send \"1\r\"; sleep 2; expect -re \"\[\/opt\/Tablet\]\"; send \"\/usr\/local\/Tablet\/\r\"; expect -re \"Yes \[y, Enter\], No \[n\]\"; send \"y\r\"; expect -re \"\[\/usr\/local\/bin\]\"; send \"\r\"; expect -re \"Yes \[y, Enter\], No \[n\]\"; send \"n\r\"; interact" \
    && chmod 777 -R /usr/local/Tablet \
    && rm /usr/local/tablet.sh

# Install htslib
########
ADD https://github.com/samtools/htslib/releases/download/1.9/htslib-1.9.tar.bz2 /usr/local/htslib.tar.bz2
RUN tar xvjf /usr/local/htslib.tar.bz2 -C /usr/local/ \
    && chmod 777 -R /usr/local/htslib-1.9 \
    && cd /usr/local/htslib-1.9 \
    && ./configure \
    && make \
    && make install \
    && rm /usr/local/htslib.tar.bz2

# Install samtools
########
ADD https://github.com/samtools/samtools/releases/download/1.9/samtools-1.9.tar.bz2 /usr/local/samtools.tar.bz2
RUN tar xvjf /usr/local/samtools.tar.bz2 -C /usr/local/ \
    && chmod 777 -R /usr/local/samtools-1.9 \
    && cd /usr/local/samtools-1.9 \
    && ./configure \
    && make \
    && make install \
    && rm /usr/local/samtools.tar.bz2

# Install picard
########
ADD https://github.com/broadinstitute/picard/releases/download/2.18.14/picard.jar /usr/local/bin/picard.jar
RUN echo -e '#!/bin/bash \n\njava -jar /usr/local/bin/picard.jar $@' > /usr/local/bin/picard \
    && chmod 777 /usr/local/bin/picard*

## Setup DeconSeq
########
COPY ./deconseq-standalone-0.4.3.tar.gz /usr/local/deconseq-standalone-0.4.3.tar.gz
COPY ./deconseq-graphs-0.1.tar.gz /usr/local/deconseq-graphs-0.1.tar.gz
RUN tar xvf /usr/local/deconseq-standalone-0.4.3.tar.gz -C /usr/local/ \
    && tar xvf /usr/local/deconseq-graphs-0.1.tar.gz -C /usr/local/
COPY ./DeconSeqConfig.pm /usr/local/deconseq-standalone-0.4.3/DeconSeqConfig.pm
RUN ln -s /usr/local/deconseq-standalone-0.4.3/*.pl /usr/local/bin/ \
    && ln -s /usr/local/deconseq-graphs-0.1/deconseq-graphs.pl /usr/local/bin/ \
    && chmod 777 -R /usr/local/deconseq* \
    && rm /usr/local/deconseq-graphs-0.1.tar.gz \
    && rm /usr/local/deconseq-standalone-0.4.3.tar.gz

############ REBECA ############

# Install bam-readcount
###
RUN git clone https://github.com/genome/bam-readcount.git /usr/local/bam-readcount \
    && cd /usr/local/bam-readcount/ \
    && chmod -R 777 /usr/local/bam-readcount/ \
    && cd /usr/local/bam-readcount/ \
    && cmake ./ \
    && make

# Install HISAT2
###
ADD http://ccb.jhu.edu/software/hisat2/dl/hisat2-2.1.0-Linux_x86_64.zip /usr/local/hisat2.zip
RUN unzip /usr/local/hisat2.zip -d /usr/local/ \
    && chmod 777 -R /usr/local/hisat2-2.1.0 \
    && ln -s /usr/local/hisat2-2.1.0/hisat* /usr/local/bin/ \
    && rm /usr/local/hisat2.zip

# Install StringTie
###
ADD http://ccb.jhu.edu/software/stringtie/dl/stringtie-1.3.5.Linux_x86_64.tar.gz /usr/local/stringtie.tar.gz
RUN tar -xzvf /usr/local/stringtie.tar.gz -C /usr/local/ \
    && chmod 777 -R /usr/local/stringtie-1.3.5.Linux_x86_64/ \
    && ln -s /usr/local/stringtie-1.3.5.Linux_x86_64/stringtie /usr/local/bin/ \
    && rm /usr/local/stringtie.tar.gz

# Install gffcompare
###
ADD http://ccb.jhu.edu/software/stringtie/dl/gffcompare-0.10.6.Linux_x86_64.tar.gz /usr/local/gffcompare.tar.gz
RUN tar -xzvf /usr/local/gffcompare.tar.gz -C /usr/local/ \
    && chmod 777 -R /usr/local/gffcompare-0.10.6.Linux_x86_64 \
    && ln -s /usr/local/gffcompare-0.10.6.Linux_x86_64/gffcompare /usr/local/bin/ \
    && rm /usr/local/gffcompare.tar.gz

# Install htseq-count
###
RUN pip install -U HTSeq \
    && pip3 install -U HTSeq

# Install TopHat
###
ADD https://ccb.jhu.edu/software/tophat/downloads/tophat-2.1.1.Linux_x86_64.tar.gz /usr/local/tophat.tar.gz
RUN tar -zxvf /usr/local/tophat.tar.gz -C /usr/local/ \
    && chmod 777 -R /usr/local/tophat-2.1.1.Linux_x86_64 \
    && cd /usr/local/tophat-2.1.1.Linux_x86_64 \
    && rm AUTHORS README LICENSE \
    && ln -s /usr/local/tophat-2.1.1.Linux_x86_64/* /usr/local/bin/ \
    && rm /usr/local/tophat.tar.gz

# Install kallisto
###
ADD https://github.com/pachterlab/kallisto/releases/download/v0.44.0/kallisto_linux-v0.44.0.tar.gz /usr/local/kallisto.tar.gz
RUN tar -zxvf /usr/local/kallisto.tar.gz -C /usr/local/ \
    && chmod 777 -R /usr/local/kallisto_linux-v0.44.0 \
    && ln -s /usr/local/kallisto_linux-v0.44.0/kallisto /usr/local/bin/ \
    && rm /usr/local/kallisto.tar.gz

# Install MultiQC
###
RUN pip3 install -U multiqc

# Install Flexbar
###
ADD https://github.com/seqan/flexbar/releases/download/v3.4.0/flexbar-3.4.0-linux.tar.gz /usr/local/flexbar.tar.gz
RUN tar -xzvf /usr/local/flexbar.tar.gz -C /usr/local/ \
    && chmod 777 -R /usr/local/flexbar-3.4.0-linux \
    && export LD_LIBRARY_PATH=/usr/local/flexbar-3.4.0-linux:$LD_LIBRARY_PATH \
    && echo "export LD_LIBRARY_PATH=/usr/local/flexbar-3.4.0-linux:$LD_LIBRARY_PATH" >> /etc/bash.bashrc \
    && ln -s /usr/local/flexbar-3.4.0-linux/flexbar /usr/local/bin/ \
    && rm /usr/local/flexbar.tar.gz

# Install Regtools
RUN git clone https://github.com/griffithlab/regtools.git /usr/local/regtools \
    && chmod 777 -R /usr/local/regtools \
    && cd /usr/local/regtools \
    && mkdir build \
    && cd build/ \
    && cmake .. \
    && make \
    && ln -s /usr/local/regtools/build/regtools /usr/local/bin/

# Install RSeQC
###
RUN pip install -U RSeQC

# Install bedtools
###
ADD https://github.com/arq5x/bedtools2/releases/download/v2.27.1/bedtools-2.27.1.tar.gz /usr/local/bedtools-2.27.1.tar.gz
RUN tar xvf /usr/local/bedtools-2.27.1.tar.gz -C /usr/local/ \
    && chmod 777 -R /usr/local/bedtools2 \
    && cd /usr/local/bedtools2 \
    && make \
    && make install \
    && rm /usr/local/bedtools-2.27.1.tar.gz

# Install gffread
###
RUN git clone https://github.com/gpertea/gclib /usr/local/gclib \
    && git clone https://github.com/gpertea/gffread /usr/local/gffread \
    && cd /usr/local/gffread \
    && make release \
    && ln -s /usr/local/gffread/gffread /usr/local/bin/

# Install SeqMonk
###
ADD http://www.bioinformatics.babraham.ac.uk/projects/seqmonk/seqmonk_v1.43.0.zip /usr/local/seqmonk.zip
RUN unzip /usr/local/seqmonk.zip -d /usr/local/ \
    && chmod 777 -R /usr/local/SeqMonk \
    && ln -s /usr/local/SeqMonk/seqmonk /usr/local/bin/ \
    && rm /usr/local/seqmonk.zip

## Create user transcriptomics
########
RUN useradd -r -s /bin/bash -U -m -d /home/transcriptomics -p '' transcriptomics

# Setup the user environment
########
ENV HOME /home/transcriptomics
RUN usermod -aG sudo,audio,video transcriptomics \
    && echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

WORKDIR $HOME
USER transcriptomics

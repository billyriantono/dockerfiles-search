FROM crukcibioinformatics/bss-introbioc
MAINTAINER Mark Fernandes<mark.fernandes@cruk.cam.ac.uk>

# NGS_Data
#---------
RUN rm -rf /var/lib/apt/lists/*
# add contrib and non-free sources (needed for igv)
COPY etc_apt_sources.list /etc/apt/sources.list
RUN apt-get update 
RUN apt-get install --fix-missing -y git
RUN mkdir -p /home/participant/
# RUN git clone --recursive https://github.com/bioinformatics-core-shared-training/cruk-autumn-school-2017.git /home/participant/Course_Materials

# Install fastqc
WORKDIR /tmp
# RUN wget http://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.11.3.zip -P /tmp
COPY FastQC.zip fastqc.zip
RUN unzip fastqc.zip && sudo chmod 755 FastQC/fastqc
RUN ln -s $(pwd)/FastQC/fastqc /usr/bin/fastqc

# Install various alignment tools and bedtools
RUN apt-get install -y bowtie2 samtools bedtools bwa igv zlib1g-dev

## installing latest version of SRA toolkit
RUN wget -nv https://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/2.8.1-3/sratoolkit.2.8.1-3-ubuntu64.tar.gz
RUN gunzip sratoolkit.2.8.1-3-ubuntu64.tar.gz
RUN tar xvf sratoolkit.2.8.1-3-ubuntu64.tar
RUN ln -s /tmp/sratoolkit.2.8.1-3-ubuntu64/bin/* /usr/bin/

# Get STAR source using git
RUN git clone https://github.com/alexdobin/STAR.git
RUN  cd STAR/source && make STAR

## Install cutadapt 
RUN apt-get install -y python-dev
RUN wget -nv https://bootstrap.pypa.io/get-pip.py
RUN sudo python get-pip.py
RUN sudo pip install cython
RUN sudo pip install --user --upgrade cutadapt
RUN rm get-pip.py
RUN chmod +x ~/.local/bin/cutadapt
RUN ln -s ~/.local/bin/cutadapt /usr/bin/cutadapt

# Install samstat
RUN wget -nv https://sourceforge.net/projects/samstat/files/latest/samstat-1.5.1.tar.gz
RUN tar -zxvf samstat-1.5.1.tar.gz
WORKDIR samstat-1.5.1
RUN ./configure
RUN make
#RUN make check
RUN make install

# Install R packages for different sections
COPY NGS_data/install_ngs_data.R /home/participant/Course_Materials/
RUN R -f /home/participant/Course_Materials/install_ngs_data.R

#RUN rm -rf /tmp
RUN chown rstudio /home/participant/Course_Materials/
WORKDIR /home//participant/Course_Materials/

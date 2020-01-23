FROM biocorecrg/centos-perlbrew-pyenv-java:centos7

# File Author / Maintainer
MAINTAINER Luca Cozzuto <lucacozzuto@gmail.com> 

ARG BLAST_VERSION=2.2.31
ARG BWA_VERSION=0.7.15
ARG QUALIMAP_VERSION=2.2.1
ARG SKEWER_VERSION=0.2.2
ARG MULTIQC_VERSION=1.7
ARG FASTQC_VERSION=0.11.5
ARG SAMTOOLS_VERSION=1.4.1
ARG PICARD_VERSION=2.10.5
ARG VEP_VERSION=89.7
ARG HTSLIB_VERSION=1.4.1
ARG BCFTOOLS_VERSION=1.4.1
ARG BEDTOOLS_VERSION=2.26.0
ARG SNPEFF_VERSION=4_3p

#INSTALLING BLAST
RUN bash -c 'curl -k -L ftp://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/${BLAST_VERSION}/ncbi-blast-${BLAST_VERSION}+-x64-linux.tar.gz > blast.tar.gz'
RUN tar -zvxf blast.tar.gz
RUN mv ncbi-blast-${BLAST_VERSION}+/bin/* /usr/local/bin/

#INSTALLING BWA
RUN bash -c 'curl -k -L https://sourceforge.net/projects/bio-bwa/files/bwa-${BWA_VERSION}.tar.bz2/download > bwa.tar.bz2'
RUN tar -jvxf bwa.tar.bz2
RUN cd bwa-${BWA_VERSION}; make; ln -s $PWD/bwa /usr/local/bin/bwa ; cd ../

#INSTALLING FASTQC
RUN bash -c 'curl -k -L https://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v${FASTQC_VERSION}.zip > fastqc.zip'

RUN unzip fastqc.zip; chmod 775 FastQC/fastqc; ln -s $PWD/FastQC/fastqc /usr/local/bin/fastqc


# Installing QUALIMAP
RUN bash -c 'curl -k -L https://bitbucket.org/kokonech/qualimap/downloads/qualimap_v${QUALIMAP_VERSION}.zip > qualimap.zip'
RUN unzip qualimap.zip

RUN ln -s $PWD/qualimap_v${QUALIMAP_VERSION}/qualimap /usr/local/bin/

# Installing MULTIQC_VERSION // Latest dev version is much better. 
RUN pip install -Iv https://github.com/ewels/MultiQC/archive/v${MULTIQC_VERSION}.tar.gz 
#RUN pip install --upgrade --force-reinstall git+https://github.com/ewels/MultiQC.git 

# Installing Skewer
RUN bash -c 'curl -k -L https://downloads.sourceforge.net/project/skewer/Binaries/skewer-${SKEWER_VERSION}-linux-x86_64 > /usr/local/bin/skewer'
RUN chmod +x /usr/local/bin/skewer

# Installing HTSLIB
RUN yum install -y zlib-devel bzip2-devel xz-devel
RUN bash -c 'curl -k -L https://github.com/samtools/htslib/releases/download/${HTSLIB_VERSION}/htslib-${HTSLIB_VERSION}.tar.bz2 > htslib.tar.bz2'
RUN tar -jvxf htslib.tar.bz2
RUN cd htslib-${HTSLIB_VERSION}; ./configure; make; make install; cd ../

# Installin BCF TOOLS
RUN bash -c 'curl -k -L https://github.com/samtools/bcftools/releases/download/${BCFTOOLS_VERSION}/bcftools-${BCFTOOLS_VERSION}.tar.bz2 > bcftools.tar.bz2'
RUN tar -jvxf bcftools.tar.bz2
RUN cd bcftools-${BCFTOOLS_VERSION}; make; make install; cd ../

# Installing samtools
RUN yum install -y xz-devel.x86_64
RUN bash -c 'curl -k -L https://downloads.sourceforge.net/project/samtools/samtools/${SAMTOOLS_VERSION}/samtools-${SAMTOOLS_VERSION}.tar.bz2 > samtools.tar.bz2'
RUN tar -jvxf samtools.tar.bz2
RUN cd samtools-${SAMTOOLS_VERSION}; ./configure; make; make install; cd ../

#Installing Picard
RUN bash -c 'curl -k -L https://github.com/broadinstitute/picard/releases/download/${PICARD_VERSION}/picard.jar > /usr/local/bin/picard.jar'
ENV PICARD=/usr/local/bin/picard.jar

#INSTALLING VEP
RUN cpanm Set::IntervalTree 
RUN cpanm JSON 
RUN cpanm PerlIO::gzip 
RUN cpanm DBI
RUN yum install -y libxml2-devel.x86_64 perl-GD.x86_64 which gd-devel.x86_64
RUN cpanm Bio::DB::HTS::Tabix
RUN bash -c 'curl -k -L https://github.com/Ensembl/ensembl-vep/archive/release/${VEP_VERSION}.tar.gz > vep.tar.gz'
RUN tar -zvxf vep.tar.gz
RUN cd ensembl-vep-release-${VEP_VERSION}; perl INSTALL.pl -a a; ln -s $PWD/vep /usr/local/bin/vep; cd ../

#Installing snpEff
RUN bash -c 'curl -k -L https://sourceforge.net/projects/snpeff/files/snpEff_v${SNPEFF_VERSION}_core.zip/download > snpEff.zip'
RUN unzip snpEff.zip
ENV SNPEFF_CONFIG=/project/snpEff/snpEff.config 
ENV SNPEFF=/project/snpEff/snpEff.jar

# Installing bedtools 
RUN bash -c 'curl -k -L https://github.com/arq5x/bedtools2/releases/download/v${BEDTOOLS_VERSION}/bedtools-${BEDTOOLS_VERSION}.tar.gz > bedtools.tar.gz'
RUN tar -zvxf bedtools.tar.gz
RUN cd bedtools2; make; cp ./bin/* /usr/local/bin/

#adding a make_window_splitter perl script
COPY scripts/make_genomic_windows.pl /usr/local/bin/make_genomic_windows.pl 

#Improving samtools sort
COPY scripts/samsort.sh /usr/local/bin/samsort.sh

# Clean cache
RUN yum clean all 

#cleaning
RUN rm -fr *.tar.gz; rm -fr *.bz2

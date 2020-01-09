# Dockerfile created 5/25/2018
# This dockerfile will take smccalla/amplicon_dockerfile and make a new one
# that has bbmap, 12s ref fasta and taxonomy files installed in /usr/local/bin/
# To build, run: docker build --rm --force-rm -t ylor/qiime1_amplicon .
# smccalla/amplicon_dockerfile has the following programs already:
# BLAST 2.6.0
# Biopython
# fastQValidator
# FastQC
# Qiime1
# Taxonomy Assignment
# Trimmomatic
# 6/12/2018: updated to copy over step1 and step2 scripts to /usr/local/bin/

FROM smccalla/amplicon_dockerfile

#RUN conda install -c bioconda java-jdk

# Download and install BBMap
WORKDIR /root/
RUN cd ~ && \
    wget http://downloads.sourceforge.net/project/bbmap/BBMap_37.97.tar.gz && \
    tar -xxvf BBMap_37.97.tar.gz && \
    cp -r bbmap/ /usr/local/bin/ && \
	rm -rf BBMap_37.97.tar.gz bbmap
ENV PATH "$PATH:/usr/local/bin/bbmap"
ENV PATH /usr/local/bin/bbmap:$PATH

COPY step1_06082018.py /usr/local/bin/
ENV PATH "$PATH:/usr/local/bin/step1_06082018.py"
ENV PATH /usr/local/bin/step1_06082018.py:$PATH

COPY step2_06082018.py /usr/local/bin/
ENV PATH "$PATH:/usr/local/bin/step2_06082018.py"
ENV PATH /usr/local/bin/step2_06082018.py:$PATH







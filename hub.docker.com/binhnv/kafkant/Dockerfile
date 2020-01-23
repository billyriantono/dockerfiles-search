FROM binfgsc/base-java:latest

################## MAINTAINER ######################
LABEL maintainer.name="William Hargreaves"
LABEL maintainer.email="whargrea@uoguelph.ca"

################## INSTALLATION ######################
# install perl and ttf-dejavu which contains fonts for the fastqc report
# (alpine lacks all fonts)
RUN sudo apk --no-cache add perl ttf-dejavu

# FASTQC
ENV URL=http://www.bioinformatics.babraham.ac.uk/projects/fastqc
ENV ZIP=fastqc_v0.11.8.zip

RUN wget $URL/$ZIP -P /opt && \
    unzip /opt/$ZIP -d /opt && \
    rm /opt/$ZIP && \
    chmod 755 /opt/FastQC/fastqc && \
    sudo ln -s /opt/FastQC/fastqc /usr/local/bin/fastqc


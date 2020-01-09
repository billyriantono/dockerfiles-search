FROM seppinho/mtdna-server

MAINTAINER Lukas Forer <lukas@forer.it>


# Change user to root
USER root

RUN apt-get update && \
    apt-get install -y \
      pkg-config && \
    apt-get clean && \
    apt-get purge && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN URL=https://github.com/vcftools/vcftools/releases/download/v0.1.14/ && \
    ZIP=vcftools-0.1.14.tar.gz && \
    FOLDER=vcftools-0.1.14 && \
    DST=/tmp && \
    wget $URL/$ZIP -O $DST/$ZIP && \
    tar xvf $DST/$ZIP -C $DST && \
    rm $DST/$ZIP && \
    cd $DST/$FOLDER && \
    ./configure && \
    make && \
    make install && \
    cd / && \
    rm -rf $DST/$FOLDER

#Change user to cloudgene
USER cloudgene
   
# change the work dir back to opt
WORKDIR /opt

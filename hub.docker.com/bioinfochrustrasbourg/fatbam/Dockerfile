FROM centos
MAINTAINER Antony Le Bechec <antony.lebechec@gmail.com>

##############################################################
# Dockerfile Version:   1.0
# Software:             FATBAM
# Software Version:     0.9.9b
# Software Website:     https://gitlab.bioinfo-diag.fr/lebechec/FATBAM
# Description:          FATBAM
##############################################################


#######
# YUM #
#######

#RUN yum update -y
RUN yum install -y java-1.8.0 \
                  zlib-devel zlib \
                  zlib2-devel zlib2 \
                  bzip2-devel bzip2 \
                  lzma-devel lzma \
                  xz-devel xz \
                  ncurses-devel \
                  wget \
                  gcc \
                  gcc-c++ \
                  make \
                  perl \
                  perl-Switch \
                	perl-Digest-MD5 \
                	perl-Data-Dumper \
                  bc ;
RUN yum clean all ;


##########
# HTSLIB #
##########

ENV TOOLS=/home/TOOLS/tools
ENV TOOL_NAME=htslib
ENV TOOL_VERSION=1.8
ENV TARBALL_LOCATION=https://github.com/samtools/$TOOL_NAME/releases/download/$TOOL_VERSION/
ENV TARBALL=$TOOL_NAME-$TOOL_VERSION.tar.bz2
ENV DEST=$TOOLS/$TOOL_NAME/$TOOL_VERSION
ENV PATH=$TOOLS/$TOOL_NAME/$TOOL_VERSION/bin:$PATH

# INSTALL
RUN wget $TARBALL_LOCATION/$TARBALL ; \
    tar xf $TARBALL ; \
    rm -rf $TARBALL ; \
    cd $TOOL_NAME-$TOOL_VERSION ; \
    make prefix=$TOOLS/$TOOL_NAME/$TOOL_VERSION install ; \
    cd ../ ; \
    rm -rf $TOOL_NAME-$TOOL_VERSION ; \
    ln -s $TOOLS/$TOOL_NAME/$TOOL_VERSION $TOOLS/$TOOL_NAME/current


############
# BCFTOOLS #
############

ENV TOOLS=/home/TOOLS/tools
ENV TOOL_NAME=bcftools
ENV TOOL_VERSION=1.8
ENV TARBALL_LOCATION=https://github.com/samtools/$TOOL_NAME/releases/download/$TOOL_VERSION/
ENV TARBALL=$TOOL_NAME-$TOOL_VERSION.tar.bz2
ENV DEST=$TOOLS/$TOOL_NAME/$TOOL_VERSION
ENV PATH=$TOOLS/$TOOL_NAME/$TOOL_VERSION/bin:$PATH

# INSTALL
RUN wget $TARBALL_LOCATION/$TARBALL ; \
    tar xf $TARBALL ; \
    rm -rf $TARBALL ; \
    cd $TOOL_NAME-$TOOL_VERSION ; \
    make prefix=$TOOLS/$TOOL_NAME/$TOOL_VERSION install ; \
    cd ../ ; \
    rm -rf $TOOL_NAME-$TOOL_VERSION ; \
    ln -s $TOOLS/$TOOL_NAME/$TOOL_VERSION $TOOLS/$TOOL_NAME/current


############
# SAMTOOLS #
############

ENV TOOLS=/home/TOOLS/tools
ENV TOOL_NAME=samtools
ENV TOOL_VERSION=1.8
ENV TARBALL_LOCATION=https://github.com/samtools/$TOOL_NAME/releases/download/$TOOL_VERSION/
ENV TARBALL=$TOOL_NAME-$TOOL_VERSION.tar.bz2
ENV DEST=$TOOLS/$TOOL_NAME/$TOOL_VERSION
ENV PATH=$TOOLS/$TOOL_NAME/$TOOL_VERSION/bin:$PATH

# INSTALL
RUN wget $TARBALL_LOCATION/$TARBALL ; \
    tar xf $TARBALL ; \
    rm -rf $TARBALL ; \
    cd $TOOL_NAME-$TOOL_VERSION ; \
    make prefix=$TOOLS/$TOOL_NAME/$TOOL_VERSION install ; \
    cd ../ ; \
    rm -rf $TOOL_NAME-$TOOL_VERSION ; \
    ln -s $TOOLS/$TOOL_NAME/$TOOL_VERSION $TOOLS/$TOOL_NAME/current



############
# BEDTOOLS #
############

ENV TOOLS=/home/TOOLS/tools
ENV TOOL_NAME=bedtools
ENV TOOL_VERSION=2.27.1
ENV TARBALL_LOCATION=https://github.com/arq5x/bedtools2/releases/download/v$TOOL_VERSION
ENV TARBALL=$TOOL_NAME-$TOOL_VERSION.tar.gz
ENV TARBALL_FOLDER=bedtools2
ENV DEST=$TOOLS/$TOOL_NAME/$TOOL_VERSION
ENV PATH=$TOOLS/$TOOL_NAME/$TOOL_VERSION/bin:$PATH

# INSTALL
RUN wget $TARBALL_LOCATION/$TARBALL ; \
    tar xf $TARBALL ; \
    rm -rf $TARBALL ; \
    cd $TARBALL_FOLDER ; \
    make prefix=$TOOLS/$TOOL_NAME/$TOOL_VERSION install ; \
    cd ../ ; \
    rm -rf $TARBALL_FOLDER ; \
    ln -s $TOOLS/$TOOL_NAME/$TOOL_VERSION $TOOLS/$TOOL_NAME/current ;


##########
# PICARD #
##########

ENV TOOLS /home/TOOLS/tools
ENV TOOL_NAME picard
ENV TOOL_VERSION 2.18.5
ENV JAR_LOCATION https://github.com/broadinstitute/picard/releases/download/$TOOL_VERSION
ENV JAR picard.jar
ENV DEST $TOOLS/$TOOL_NAME/$TOOL_VERSION
ENV PATH "$TOOLS/$TOOL_NAME/$TOOL_VERSION/bin:$PATH"

# INSTALL
RUN wget $JAR_LOCATION/$JAR ; \
    mkdir -p $TOOLS/$TOOL_NAME/$TOOL_VERSION/bin ; \
    mv $JAR $TOOLS/$TOOL_NAME/$TOOL_VERSION/bin ; \
    ln -s $TOOLS/$TOOL_NAME/$TOOL_VERSION/bin/$JAR /$JAR ; \
    ln -s $TOOLS/$TOOL_NAME/$TOOL_VERSION $TOOLS/$TOOL_NAME/current ;


##########
# FATBAM #
##########

# https://gitlab.bioinfo-diag.fr/lebechec/FATBAM/repository/0.9.9b/archive.tar.gz
# https://gitlab.bioinfo-diag.fr/lebechec/FATBAM/repository/0.9.9b/archive.tar.gz


ENV TOOLS=/home/TOOLS/tools
ENV TOOL_NAME=fatbam
ENV TOOL_VERSION=0.9.9b
ENV TARBALL_LOCATION=https://gitlab.bioinfo-diag.fr/lebechec/FATBAM/repository/0.9.9b
ENV TARBALL=archive.tar.gz
ENV TARBALL_FOLDER=archive
ENV DEST=$TOOLS/$TOOL_NAME/$TOOL_VERSION
ENV PATH=$TOOLS/$TOOL_NAME/$TOOL_VERSION/bin:$PATH

# INSTALL
RUN wget $TARBALL_LOCATION/$TARBALL ; \
    tar xf $TARBALL ; \
    rm -rf $TARBALL ; \
    mkdir -p $TOOLS/$TOOL_NAME/$TOOL_VERSION/ ; \
    cp $(ls ${TOOL_NAME^^}-$TOOL_VERSION* -d)/* $TOOLS/$TOOL_NAME/$TOOL_VERSION/ -R ; \
    rm -rf $(ls ${TOOL_NAME^^}-$TOOL_VERSION* -d) ; \
    ln -s $TOOLS/$TOOL_NAME/$TOOL_VERSION $TOOLS/$TOOL_NAME/current ; \
    chmod 0775 $TOOLS/$TOOL_NAME/$TOOL_VERSION $TOOLS/$TOOL_NAME/current -R ;


#######
# YUM #
#######

RUN yum erase -y zlib-devel \
                  zlib2-devel \
                  bzip2-devel \
                  lzma-devel \
                  xz-devel \
                  ncurses-devel \
                  wget \
                  gcc \
                  gcc-c++ ;
RUN yum clean all ;

WORKDIR "$TOOLS/$TOOL_NAME/current/bin"

CMD ["/bin/bash"]

FROM comics/centos
MAINTAINER Ian Merrick <MerrickI@Cardiff.ac.uk>

##############################################################
# Dockerfile Version:   0.1
# Software:             samtools
# Software Version:     1.9
# Software Website:     https://github.com/samtools/samtools/
# Description:          samtools
##############################################################

ENV APP_NAME=samtools
ENV VERSION=1.9
ENV GIT=https://github.com/BenLangmead/samtools.git
ENV APPS=/software/applications
ENV DEST=$APPS/$APP_NAME/
ENV PATH=$APPS/$APP_NAME/$VERSION/bin:$APPS/bcftools/$VERSION/bin:$PATH

RUN yum install -y bzip2-devel \
                   ncurses-devel \
                   xz-devel \
                   zlib-devel && \
    yum clean all 
RUN curl -L https://github.com/samtools/htslib/archive/$VERSION.tar.gz | tar xz && \
    curl -L https://github.com/samtools/samtools/archive/$VERSION.tar.gz | tar xz && \
    curl -L https://github.com/samtools/bcftools/archive/$VERSION.tar.gz | tar xz && \
    mv htslib-$VERSION htslib && \ 
    cd bcftools-$VERSION && \
    make -j HTSDIR=../htslib && \
    make prefix=$APPS/bcftools/$VERSION install && \
    cd .. && \
    cd samtools-$VERSION && \
    make -j HTSDIR=../htslib && \
    make prefix=$APPS/$APP_NAME/$VERSION install && \
    cd ../ && \
    rm -rf htslib samtools-$VERSION bcftools-$VERSION

CMD ["/bin/bash"]


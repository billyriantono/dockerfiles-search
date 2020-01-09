# Dockerfile created 7/24/2019 Yer Lor
# This Dockerfile takes the qiime2/core:2019.4 docker image.

FROM qiime2/core:2019.4

#RUN conda install -c bioconda java-jdk
#RUN apt-get update && apt-get upgrade -y --force-yes && apt-get install -y git $

# Download and install BBMap
WORKDIR /root/
RUN cd ~ && \
    wget http://downloads.sourceforge.net/project/bbmap/BBMap_37.97.tar.gz && \
    tar -zxvf BBMap_37.97.tar.gz && \
    cp -r bbmap/ /usr/local/bin/ && \
    rm -rf BBMap_37.97.tar.gz bbmap
ENV PATH "$PATH:/usr/local/bin/bbmap"
ENV PATH /usr/local/bin/bbmap:$PATH

# Install kent-utils
# http://hgdownload.soe.ucsc.edu/admin/exe/linux.x86_64/
WORKDIR /root/
RUN cd ~ && \
    rsync -aP rsync://hgdownload.soe.ucsc.edu/genome/admin/exe/linux.x86_64/ /u$
ENV PATH "$PATH:/usr/local/bin/kent-utils"
ENV PATH /usr/local/bin/kent-utils:$PATH

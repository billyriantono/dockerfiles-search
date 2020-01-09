FROM ubuntu:16.04

LABEL author="Kersten Breuer, Zeller Team, EMBL 2017" \
    maintainer="kersten-breuer@outlook.com"

# Install essential unix packages and dependencies:
RUN apt-get update -y --fix-missing
RUN apt-get install -y build-essential \
    wget \
    tar
RUN apt-get update -y --fix-missing
RUN apt-get -y install openjdk-8-jdk

# Install BBMap:
ENV BBMAP_URL http://downloads.sourceforge.net/project/bbmap/BBMap_36.28.tar.gz
RUN cd /usr/local/ \
    && wget -O bbmap.tar.gz ${BBMAP_URL} \
    && tar -xvzf bbmap.tar.gz \
    && rm bbmap.tar.gz
ENV PATH="/usr/local/bbmap:${PATH}"

CMD ["bbduk.sh"]
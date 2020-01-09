FROM ubuntu:10.04
MAINTAINER Aleksey Krasnobaev <https://github.com/krasnobaev>

RUN DEBIAN_FRONTEND=noninteractive apt-get -y install wget

RUN mkdir /usr/data

# collections from Glasgow university site
RUN mkdir /usr/data/cacm; \
    cd /usr/data; wget http://ir.dcs.gla.ac.uk/resources/test_collections/cacm/cacm.tar.gz; \
    cd /usr/data/cacm; tar -xzf ../cacm.tar.gz

RUN mkdir /usr/data/lisa; cd /usr/data; \
    wget http://ir.dcs.gla.ac.uk/resources/test_collections/lisa/lisa.tar.gz; \
    cd /usr/data/lisa; tar -xzf ../lisa.tar.gz

RUN mkdir /usr/data/npl; cd /usr/data; \
    wget http://ir.dcs.gla.ac.uk/resources/test_collections/npl/npl.tar.gz; \
    cd /usr/data/npl; tar -xzf ../npl.tar.gz

RUN mkdir /usr/data/cisi; cd /usr/data; \
    wget http://ir.dcs.gla.ac.uk/resources/test_collections/cisi/cisi.tar.gz; \
    cd /usr/data/cisi; tar -xzf ../cisi.tar.gz

RUN mkdir /usr/data/cran; cd /usr/data; \
    wget http://ir.dcs.gla.ac.uk/resources/test_collections/cran/cran.tar.gz; \
    cd /usr/data/cran; tar -xzf ../cran.tar.gz

RUN mkdir /usr/data/time; cd /usr/data; \
    wget http://ir.dcs.gla.ac.uk/resources/test_collections/time/time.tar.gz; \
    cd /usr/data/time; tar -xzf ../time.tar.gz

RUN mkdir /usr/data/med; cd /usr/data; \
    wget http://ir.dcs.gla.ac.uk/resources/test_collections/medl/med.tar.gz; \
    cd /usr/data/med; tar -xzf ../med.tar.gz

RUN mkdir /usr/data/adi; cd /usr/data; \
    wget http://ir.dcs.gla.ac.uk/resources/test_collections/adi/adi.tar.gz; \
    cd /usr/data/adi; tar -xzf ../adi.tar.gz

RUN ls -l /usr/data


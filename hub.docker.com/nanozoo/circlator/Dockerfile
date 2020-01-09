FROM continuumio/miniconda3
ENV VERSION 1.5.5 

RUN apt update && apt install -y procps && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN conda config --add channels conda-forge && \
    conda config --add channels bioconda && \
    conda config --add channels default

RUN conda install circlator=$VERSION canu spades && conda clean -a

# AMOS dependency if circlator is only used for "circling"
#RUN apt-get update && apt-get install -y autotools-dev automake libqt4-dev libboost-graph-dev perl
#RUN git clone git://git.code.sf.net/p/amos/code amos-code
#RUN apt-get install -y  g++ make libzip-dev
#RUN cpan XML::Parser Config::IniFiles Statistics::Descriptive DBI
#RUN conda install -c bioconda perl-xml-parser blat perl-statistics-descriptive perl-dbi jellyfish= && conda clean -a
#RUN cd amos-code && ./bootstrap && ./configure --prefix=/usr/local/AMOS 
#RUN cd amos-code && make CXXFLAGS='-Wno-deprecated' &&  make install

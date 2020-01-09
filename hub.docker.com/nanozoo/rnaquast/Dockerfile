FROM ubuntu:xenial
ENV VERSION 1.5.2

RUN apt-get update && \
    apt-get install -y python2.7 wget python-pip cpio && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
RUN pip install --upgrade pip

RUN wget http://cab.spbu.ru/files/rnaquast/release1.5.2/rnaQUAST-1.5.2.tar.gz
RUN tar -zxvf rnaQUAST-1.5.2.tar.gz; rm *.gz

RUN pip2.7 install gffutils
RUN pip2.7 install matplotlib
RUN pip2.7 install joblib
RUN pip2.7 install biopython

RUN wget http://research-pub.gene.com/gmap/src/gmap-gsnap-2019-06-10.tar.gz
RUN tar -zxvf gmap-gsnap-2019-06-10.tar.gz; rm *.gz
RUN cd gmap-2019-06-10/; ./configure; make; make install; cd ..
ENV PATH=${PATH}:/gmap-2019-06-10/src/

RUN wget https://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/ncbi-blast+-2.9.0-src.tar.gz
RUN tar -zxvf ncbi-blast+-2.9.0-src.tar.gz; rm *.gz
RUN cd ncbi-blast-2.9.0+-src/c++/; ./configure; make; make install; cd ../..
ENV PATH=${PATH}:/gmap-2019-06-10/src/

ENV PATH=${PATH}:/rnaQUAST-1.5.2/

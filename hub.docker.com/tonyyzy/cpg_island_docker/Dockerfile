FROM frolvlad/alpine-gcc

RUN apk add curl

RUN curl -o cpg.tar.gz "http://genome-source.cse.ucsc.edu/gitweb/?p=kent.git;a=snapshot;h=b5f52d1341a04ff1329e42b1d1eae5e9f82c2174;sf=tgz"

RUN tar -xzf cpg.tar.gz

WORKDIR /kent

RUN gcc readseq.c cpg_lh.c -o cpglh

ENV PATH "$PATH:/kent"

WORKDIR /

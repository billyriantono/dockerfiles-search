FROM alpine:3.7

ENV DST=/home/
ENV URL=https://bioconductor.org/packages/release/bioc/src/contrib/

RUN wget $URL/metaseqR_1.20.0.tar.gz -O $DST/metaseqR_1.20.0.tar.gz
RUN tar -xvf $DST/metaseqR_1.20.0.tar.gz -C $DST/
RUN rm $DST/metaseqR_1.20.0.tar.gz
RUN cd  $DST/metaseqR

WORKDIR /metaseqR/

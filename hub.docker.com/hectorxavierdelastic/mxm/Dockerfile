FROM alpine:3.7

ENV DST=/home/
ENV URL=https://cran.r-project.org/src/contrib/

RUN wget $URL/MXM_1.3.5.tar.gz -O $DST/MXM_1.3.5.tar.gz
RUN tar -xvf $DST/MXM_1.3.5.tar.gz -C $DST/
RUN rm $DST/MXM_1.3.5.tar.gz
RUN cd  $DST/MXM

WORKDIR /MXM/

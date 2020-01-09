FROM alpine:latest

MAINTAINER boredpanda

##RUN echo "http://dl-8.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories
RUN apk --no-cache --update-cache add python2 python2-dev py-pip build-base gsl gsl-dev git gfortran
RUN apk --no-cache add lapack-dev
#RUN apk --no-cache add openblas-dev
RUN pip install numpy scipy ete2 pyvcf

RUN git clone https://github.com/morrislab/phylowgs.git
RUN cd phylowgs && g++ -o mh.o -O3 mh.cpp  util.cpp `gsl-config --cflags --libs`

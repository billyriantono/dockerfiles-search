FROM ubuntu:14.04

RUN apt-get update ; apt-get install gcc wget libcurl4-openssl-dev make -y ;
RUN wget http://sourceforge.net/projects/cpuminer/files/pooler-cpuminer-2.4.2.tar.gz ;
RUN tar -xvf pooler-cpuminer-2.4.2.tar.gz ;
RUN cd /cpuminer-2.4.2 ; ./configure ; make ; make install ;

CMD ["minerd", "--url=stratum+tcp://eu.multipool.us:7777", "--user", "helpdeskysmith.1", "--pass=x"]

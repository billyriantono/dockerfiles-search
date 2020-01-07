###### Image providing goPy
FROM ubuntu:13.10
MAINTAINER "Christian Kniep <christian@qnib.org>"

ADD bash_history /root/.bash_history

RUN apt-get update
RUN apt-get install -y aptitude vim
RUN aptitude upgrade -y

RUN echo "deb http://gopy.qur.me/ubuntu raring main" >> /etc/apt/sources.list
RUN apt-get update
RUN aptitude install -y gccgo-4.7 gcc-4.7 golang
RUN aptitude -o Aptitude::Cmdline::ignore-trust-violations=true install -y gopy 
RUN ln -sf /usr/bin/gcc-4.7 /usr/bin/gcc
RUN ln -sf /usr/bin/gccgo-4.7 /usr/bin/gccgo

ADD simple.go /root/
ADD simple.py /root/
ADD parallel.go /root/
ADD parallel.py /root/


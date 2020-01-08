FROM ubuntu:latest
ENV TERM linux
WORKDIR /root
RUN apt update
RUN apt install -y git
RUN apt-get update
RUN apt-get install perl 
RUN apt-get install -y lib32z1 libncurses5 uuid uuid-dev perl libssl-dev perl-doc libxml-libxml-perl libcrypt-ssleay-perl libdata-compare-perl libsoap-lite-perl
#RUN cpan install Crypt::OpenSSL::RSA UUID::Random Exception::Class Crypt::X509 List::MoreUtils
RUN git clone https://github.com/vmware/vsphere-automation-sdk-perl


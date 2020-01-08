FROM centos:centos6
LABEL maintainer "Nathaniel Watson nathankw@stanford.edu"
#Extends the centos6 library image with tools necessary for building software. 
#PURPOSE: Installs many core packages on top of the centos:centos6 base image, to allow users to be able to install further software or packages for their specific purposes. Note that since this installs teh Development Tools yum package, it automatically comes with Perl v5.10.1. However, this intallation of Perl doesn't come with cpan, cpanm, or cpanp. I was unable to install
#    cpanm using the instruction at http://search.cpan.org/~miyagawa/App-cpanminus-1.7043/lib/App/cpanminus.pm to run 
#    "curl -L https://cpanmin.us | perl - --sudo App::cpanminus". It will be best to redo the Perl install from source. 

#INSTALL some core packages.
# gcc-c++ needed for running g++ to make tools, such as Bowtie2.
# gcc needed for installing Python.
# lapack-dev blas-dev for installing scipy in Python.
# Development Tools installs 28 packages, and their dependencies. The number of dependencies installed on a base image of centos:centos6 were 101, notably of which are Perl v5.10.1, git v1.7.1, unzip
RUN yum update -y && yum groupinstall -y 'Development Tools' && yum install -y wget \
  bzip2-devel \
  lapack-devel blas-devel \
  ncurses-devel \
  openssl-devel \
  sqlite-devel \
  zlib-devel

#Make area for installing other tools that don't link into system folders, i.e. FASTQC.
RUN mkdir /srv/src /srv/software

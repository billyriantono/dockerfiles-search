FROM       adgico/gcc-4.9
MAINTAINER Byran Wills-Heath <byran@adgico.co.uk>

RUN apt-get install -y curl

RUN cd / &&\
(curl -L -k http://llvm.org/releases/3.6.2/clang+llvm-3.6.2-x86_64-linux-gnu-ubuntu-14.04.tar.xz | tar xJ) &&\
cp -r /clang+llvm-3.6.2-x86_64-linux-gnu-ubuntu-14.04/* /usr/ &&\
rm -rf /clang+llvm-3.6.2-x86_64-linux-gnu-ubuntu-14.04

RUN update-alternatives --install /usr/bin/g++ g++ /usr/bin/clang++ 20 
RUN update-alternatives --install /usr/bin/gcc gcc /usr/bin/clang 20 


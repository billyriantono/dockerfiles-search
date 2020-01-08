FROM frolvlad/alpine-glibc
MAINTAINER Lucas Hutchinson <lucas@syrp.co.nz>
LABEL Description="Image for building arm baremetal targets"
WORKDIR /work

RUN apk add --update --no-cache  \
bash \
cmake \
git \
make \
ninja \
openssh-client \
python \
tar \
wget

# Add from official source. extract and delete
RUN wget https://developer.arm.com/-/media/Files/downloads/gnu-rm/8-2018q4/gcc-arm-none-eabi-8-2018-q4-major-linux.tar.bz2
RUN tar xjf gcc-arm-none-eabi-8-2018-q4-major-linux.tar.bz2 -C /usr/local 
RUN rm -rf /work/gcc-arm-none-eabi-8-2018-q4-major-linux.tar.bz2

ENV PATH=$PATH:/usr/local/gcc-arm-none-eabi-8-2018-q4-major/bin 
RUN printenv PATH && arm-none-eabi-gcc --version

ENTRYPOINT [ "/usr/bin/bash" ]

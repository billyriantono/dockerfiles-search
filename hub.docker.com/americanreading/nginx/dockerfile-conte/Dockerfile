FROM ubuntu:trusty

RUN apt-get update && \
    apt-get -yqq install gawk wget git-core diffstat unzip texinfo gcc-multilib \
      build-essential chrpath socat libsdl1.2-dev xterm \
      subversion wget unzip python python-pip vim && \
    apt-get clean && \
    useradd -m builder && \
    echo 'builder ALL=NOPASSWD: ALL' > /etc/sudoers.d/builder
USER builder
WORKDIR /home/builder
RUN git clone git://git.yoctoproject.org/poky
RUN cd poky && git checkout krogoth && sudo pip install -r /home/builder/poky/bitbake/toaster-requirements.txt


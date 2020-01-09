FROM ubuntu:16.04

MAINTAINER Advantech

# update
RUN apt-get update
RUN apt-get install -y apt-utils sudo
RUN apt-get install -y locales curl cpio git build-essential python diffstat texinfo gawk chrpath dos2unix wget unzip socat doxygen lib32stdc++6 lib32z1 lib32ncurses5 libc6-dev-i386 gcc-multilib g++-multilib

# jenkins
RUN apt-get install -y openssh-server
RUN mkdir /var/run/sshd

# openjdk
RUN apt-get update
RUN apt-get install -y openjdk-8-jdk
# crc32
RUN apt-get install -y libarchive-zip-perl

# make /bin/sh symlink to bash instead of dash:
# To set this particular option to false:
RUN echo "dash dash/sh boolean false" | debconf-set-selections
# and to actually reconfigure the package:
RUN DEBIAN_FRONTEND=noninteractive dpkg-reconfigure dash

# adv account (password: adv)
RUN useradd -m -k /home/adv adv -p ajLGz61mdCP76 -s /bin/bash -G sudo
RUN chmod +s /usr/sbin/sshd

# set up adv as sudo
RUN echo "adv ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
WORKDIR /home/adv
USER adv

# git config
RUN git config --global user.email "you@example.com"
RUN git config --global user.name "Your Name"
RUN git config --global color.ui "auto"

# locale
RUN sudo locale-gen en_US.UTF-8
RUN sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
ENV LANG="en_US.UTF-8"

RUN wget -O "/home/adv/linux-devkit.sh" "https://sh-ctfs.ftn.qq.com/ftn_handler/3659de49c32f3d626b46bb56385cd82b7fd937a1ca31f783a1a31e77131c3487443b2d228c84a6d830e16f8e1c0d0a52194982039d34146c3df513edacfec418/?fname=linux-devkit.sh&k=263132306263b2d9867e88121538511b50535606045c56044f065105571557035b091f08050b561906060401510b530756015606333763580b5f47481e5c06420958461e40506309&code=b12038c4&fr=00&&txf_fid=4d9420b2e9d3707c41799d408d84fd0ea6bc5937&xffz=305046703"
#RUN wget -O "/home/adv/check_md5.sh" "https://sh-ctfs.ftn.qq.com/ftn_handler/85e16967eb3841e534417fd242a412c9d2e614a91bb6b3f47cdb5c1f707136833700f2ffee5701f945b2f021c779a973abbf7c1b4a48a4f7fe4e4c357fdcad26/?fname=check_md5.sh&k=78623032dfc9c7c6dd2d8a1016370a165b04035605020b0914515500041a0c0100571d5054035b14095a075351035a0f0f000854303b385a510753596f5a5c0c171158320d&code=9b020789&fr=00&&txf_fid=7d52eb08cecff887318b3ec7ec76c7b670082504&xffz=273"
#RUN ls -al
#RUN echo pwd=$PWD

RUN chmod 777 /home/adv/linux-devkit.sh
RUN sh -c '/bin/echo -e "\n\n" | sh /home/adv/linux-devkit.sh'
RUN rm /home/adv/linux-devkit.sh


# This is a comment
FROM ubuntu:14.04
MAINTAINER Yang Zhengguang zhengguang.yang@advantech.com.cn
RUN apt-get update \
	&& apt-get install -y gawk wget git-core diffstat unzip texinfo gcc-multilib build-essential chrpath socat libsdl1.2-dev xterm autoconf automake libtool libglib2.0-dev libarchive-dev git whiptail curl android-tools-fsutils doxygen dos2unix python libc6 libncurses5 libstdc++6 libz1 vim sudo ftp openssh-server openjdk-7-jdk \
	&& echo "dash dash/sh boolean false" | debconf-set-selections \
	&& DEBIAN_FRONTEND=noninteractive dpkg-reconfigure dash \
	&& mkdir /var/run/sshd \
	&& useradd -m -k /home/adv adv -p ajLGz61mdCP76 -s /bin/bash -G sudo \
	&& chmod +s /usr/sbin/sshd \
	&& echo "adv ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
WORKDIR /home/adv
USER adv
RUN git config --global user.email "you@example.com" \
	&& git config --global user.name "Your Name" \
	&& git config --global color.ui "auto" \
	&& mkdir -p ${HOME}/bin \
	&& git clone https://gerrit-googlesource.lug.ustc.edu.cn/git-repo \
	&& cp git-repo/repo ${HOME}/bin \
	&& chmod a+x ${HOME}/bin/repo \
	&& mkdir -p ${HOME}/bin/.repo \
	&& mv git-repo ${HOME}/bin/.repo/repo
ENV PATH="/home/adv/bin:${PATH}"
RUN wget https://releases.linaro.org/components/toolchain/binaries/5.3-2016.02/arm-linux-gnueabihf/gcc-linaro-5.3-2016.02-x86_64_arm-linux-gnueabihf.tar.xz \
	&& tar -Jxvf gcc-linaro-5.3-2016.02-x86_64_arm-linux-gnueabihf.tar.xz -C $HOME \
	&& rm $HOME/gcc-linaro-5.3-2016.02-x86_64_arm-linux-gnueabihf.tar.xz
ENV PATH="/home/adv/gcc-linaro-5.3-2016.02-x86_64_arm-linux-gnueabihf/bin:$PATH"
 


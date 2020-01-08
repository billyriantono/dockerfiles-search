FROM ubuntu:16.04

RUN sed -i "s/security.ubuntu.com/mirrors.tuna.tsinghua.edu.cn/g" /etc/apt/sources.list \
	&& sed -i "s/archive.ubuntu.com/mirrors.tuna.tsinghua.edu.cn/g" /etc/apt/sources.list \
	&& apt-get update && apt-get install -y \
	repo ccache openjdk-8-jdk android-tools-adb bc bison build-essential curl flex g++-multilib gcc-multilib gnupg gperf imagemagick lib32ncurses5-dev lib32readline-dev lib32z1-dev libesd0-dev liblz4-tool libncurses5-dev libsdl1.2-dev libssl-dev libwxgtk3.0-dev libxml2 libxml2-utils lzop pngcrush rsync schedtool squashfs-tools xsltproc yasm zip zlib1g-dev

RUN apt-get install -y \
	vim

RUN apt-get clean \
	&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN echo "export USER=root" >> /root/.bashrc \
	&& echo "#export ANDROID_JACK_VM_ARGS=\"-Xmx8g -Dfile.encoding=UTF-8 -XX:+TieredCompilation\"" >> /root/.bashrc \
	&& echo "#export USE_CCACHE=1" >> /root/.bashrc

COPY .gitconfig /root/

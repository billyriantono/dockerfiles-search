FROM		ubuntu:18.04
MAINTAINER	Ji-Hun Kim jihuun.k@gmail.com

# Update sources.list for fix the fetch fail issue about archive.ubuntu.com
# E: Failed to fetch http://archive.ubuntu.com/ubuntu/dists/bionic-updates/main/binary-amd64/by-hash/SHA256/03ff162217842bb22e56dabaaf3542902da8958c5dbdac7baf243227818f25ce  Hash Sum mismatch
RUN		sed -i 's/archive.ubuntu.com/kr.archive.ubuntu.com/g' /etc/apt/sources.list
RUN		apt-get -y -q upgrade
RUN		apt-get -y -q update

RUN		apt-get install -y git vim python3 python3-pip fonts-nanum
		# for python open cv error
RUN		apt-get install -y libsm6 libxext6 libxrender-dev
		# setting utf-8 locale
RUN		apt-get install -y locales
RUN		locale-gen ko_KR.UTF-8
ENV		LC_ALL ko_KR.UTF-8

RUN		git clone https://github.com/captube/youtube_capture.git
RUN		pip3 install -r youtube_capture/requirements.txt

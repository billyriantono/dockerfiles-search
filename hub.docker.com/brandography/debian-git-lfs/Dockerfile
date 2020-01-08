FROM debian:jessie

RUN apt-get update \
	&& apt-get install curl -y \
	&& curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | bash \
	&& apt-get install git-lfs -y

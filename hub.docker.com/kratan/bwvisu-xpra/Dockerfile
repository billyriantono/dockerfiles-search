FROM kratan/bwvisu-nvidiacuda:centos7

#Setup Xpra
RUN rpm --import https://winswitch.org/gpg.asc \
	&& cd /etc/yum.repos.d/ \
	&& yum -y install curl \
	&& curl -O https://winswitch.org/downloads/CentOS/winswitch.repo \
	&& yum repolist \
	&& yum -y clean all \
	&& yum -y install \
	          pangox-compat \
		  xpra \
		  perl \
	&& yum -y update

COPY entrypoint.d/ /entrypoint.d/

EXPOSE 14500

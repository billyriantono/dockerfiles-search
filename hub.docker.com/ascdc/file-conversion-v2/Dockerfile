FROM ascdc/file-conversion
MAINTAINER ASCDC <asdc.sinica@gmail.com>

RUN apt-get update && \
	DEBIAN_FRONTEND=noninteractive && \
	apt-get update -yyq && \
	apt-get dist-upgrade -yyq && \
	apt-get install -yyq jq rsync sshpass git wget curl vim apt-utils software-properties-common sudo tzdata locales language-pack-zh-hant language-pack-zh-hant-base exiftool && \
	ln -fs /usr/share/zoneinfo/Asia/Taipei /etc/localtime && \
	dpkg-reconfigure --frontend noninteractive tzdata && \
	echo "locales locales/default_environment_locale select zh_TW.UTF-8" | debconf-set-selections && \
	echo "locales locales/locales_to_be_generated multiselect zh_TW.UTF-8 UTF-8" | debconf-set-selections && \
	rm -f "/etc/locale.gen" && \
	dpkg-reconfigure --frontend noninteractive locales && \
	locale-gen en_US.UTF-8 && \
	export LANG=zh_TW.UTF-8 && \
	export LC_ALL=zh_TW.UTF-8 && \
	echo "export LANG=zh_TW.UTF-8" >> ~/.bashrc && \
	echo "export LC_ALL=zh_TW.UTF-8" >> ~/.bashrc

ENV AUTHORIZED_KEYS **None**
EXPOSE 22

WORKDIR /script
ENTRYPOINT ["/script/run.sh"]

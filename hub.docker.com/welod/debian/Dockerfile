FROM	debian:stable

RUN		mv /etc/apt/sources.list /etc/apt/sources.list.bak		\
	&&	echo 'deb http://mirrors.ustc.edu.cn/debian stable main contrib non-free' > /etc/apt/sources.list		\
	&&	echo 'deb http://mirrors.ustc.edu.cn/debian-security stable/updates main contrib non-free' >> /etc/apt/sources.list		\
	&&	echo 'deb http://mirrors.ustc.edu.cn/debian stable-updates main contrib non-free' >> /etc/apt/sources.list		\
	&&	apt-get update -qq		\
	&&	apt-get install locales -qqy		\
	&&	rm -rf /var/lib/apt/lists/*		\
	&&	localedef -i zh_CN -c -f UTF-8 -A /usr/share/locale/locale.alias zh_CN.UTF-8		\
	&&	update-locale LANG=zh_CN.UTF-8 LANGUAGE=zh_CN:zh		\
	&&	echo 'Asia/Shanghai' > /etc/timezone		\
	&&	ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime		\
	&&	dpkg-reconfigure --frontend noninteractive tzdata		\
	&&	rm -rf /root/.bash_history
ENV		LANG		zh_CN.UTF-8
ENV		LANGUAGE	zh_CN:zh

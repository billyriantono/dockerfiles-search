FROM ubuntu:14.04.5

# Install packages

WORKDIR /var/www/clsi-sharelatex

ADD locale.gen /etc/locale.gen
ADD locale-archive /usr/lib/locale/locale-archive
ADD run.sh /run.sh
RUN chmod +x /*.sh
	 
RUN DEBIAN_FRONTEND=noninteractive apt-get update && apt-get --force-yes -y install locales curl wget python build-essential zlib1g-dev fontconfig git && \
	curl -sL https://deb.nodesource.com/setup | sudo bash - && \
	apt-get update && apt-get --force-yes -y upgrade && apt-get --force-yes -y install nodejs vim latexmk texlive-xetex latex-cjk-all && \
	locale-gen zh_TW.UTF-8 && \
	dpkg-reconfigure locales && \
	echo "export LANG=zh_TW.UTF-8" >> /root/.profile && \ 
	echo "export LANGUAGE=zh_TW" >> /root/.profile && \
	echo "export LC_ALL=zh_TW.UTF-8" >> /root/.profile && \
	git clone "https://github.com/sharelatex/clsi-sharelatex.git" /var/www/clsi-sharelatex && \
	npm install && \
	npm install -g grunt-cli && \
	grunt install
	
ENV LANG zh_TW.UTF-8
ENV LANGUAGE zh_TW
ENV LC_ALL zh_TW.UTF-8
ENV AUTHORIZED_KEYS **None**

EXPOSE 80
ENTRYPOINT ["/run.sh",""]
FROM edwinek/alpine-git:3.8

RUN mkdir /opt \
	&& wget -qO- https://github.com/jgm/pandoc/releases/download/2.3.1/pandoc-2.3.1-linux.tar.gz | tar xvz -C /opt \
	&& ln -s /opt/pandoc-2.3.1/bin/pandoc /usr/bin/pandoc
